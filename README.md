# Computer Vision Algorithms

Implementation and analysis of classical computer vision algorithms, with emphasis on
algorithmic understanding, parameter selection, and failure-mode analysis.

The repository focuses on implementing core vision pipelines and analyzing their behavior
under different conditions, rather than relying on black-box library functions.

---

## Algorithms Implemented and Analyzed

- Convolution-based image filtering  
- Histogram equalization  
- Edge detection pipelines (Sobel, Canny, Non-Maximum Suppression)  
- Harris corner detection  
- Template matching methods (SAD, SSD, ZNCC)
  
- ##  Visualization

## Canny Edge Detection (Manual Implementation)
This section demonstrates a complete, step-by-step implementation of the **Canny Edge Detection** algorithm using only NumPy. Building the pipeline from scratch ensures full control over the mathematical transformations and thresholding logic.

### The Pipeline Breakdown
* **Grayscale Conversion:** The initial step of converting the input image to a single-channel luminance map to prepare for gradient analysis.
* **Gaussian Smoothing:** Manual convolution using a Gaussian kernel to reduce high-frequency noise.
* **Sobel Gradients:** Computing G_x and G_y to derive the edge magnitude and precise orientation maps.
* **Non-Maximum Suppression (NMS):** Geometric thinning of edges by analyzing pixel peaks along the gradient direction.
* **Hysteresis Thresholding:** Finalizing the binary edge map by identifying strong edges and connecting relevant weak edges.

### Visual Pipeline Step-by-Step

| 1. Original Grayscale | 2. Sobel X/Y Responses | 3. Gradient Magnitude |
| :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/ccdf4d3d-129c-464f-93e4-39e19dad3452" width="280" /> | <img src="https://github.com/user-attachments/assets/07002550-40a9-4a6e-8885-330534e97780" width="280" /> | <img src="https://github.com/user-attachments/assets/acfe5851-4b93-4e7f-b602-6189d4f96286" width="280" /> |

| 4. Gradient Orientation | 5. After NMS (Thinning) | 6. Double Thresholding |
| :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/5751ab33-f9e1-4bef-9725-3e8c0945748c" width="280" /> | <img src="https://github.com/user-attachments/assets/392de44d-6f3e-4ab6-a2ee-09ea61e147f1" width="280" /> | <img src="https://github.com/user-attachments/assets/d5711899-30f2-4b44-abc9-15c4da546272" width="280" /> |

### Final Result
| Original Image | Final Canny Edge Map |
| :---: | :---: |
| <img src="https://github.com/user-attachments/assets/ccdf4d3d-129c-464f-93e4-39e19dad3452" width="380" /> | <img src="https://github.com/user-attachments/assets/896ae1bc-e720-4a91-b2cb-0965440bae80" width="380" /> |

---

## Template Matching in Action
To demonstrate the algorithms, I used a "Mario" environment to detect coins. This illustrates how the template matching methods (SAD, SSD, ZNCC) perform.

### 1. Target & Initial Detection
The workflow begins by defining a specific target template and evaluating detection performance on the original map layout.

| Target Template | Original Map | SAD,SSD,ZNCC the same Detection Result |
| :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/4b7b4f22-fc61-443f-85be-94196a85d27c" width="60" alt="Coin Template" /> | <img src="https://github.com/user-attachments/assets/921a761c-c021-4506-b355-4cc21802e10b" width="280" alt="Original Map" /> | <img src="https://github.com/user-attachments/assets/b3e2b5b8-4d0b-434b-a7c0-f4181406f67a" width="280" alt="SAD Detection" /> |

### 2. Performance Analysis: Custom Implementation Robustness
Evaluating my **custom implementations** of matching algorithms across 10 different environments ([see data folder](https://github.com/yuvalSig/computer-vision-algorithms/tree/main/template_matching/data/mario-bonusarea)). This test analyzes how each logic handles variations in **brightness, contrast, and resolution**.
### Visual Example:
| SAD Detection | SSD Detection | ZNCC Detection |
| :---: | :---: | :---: |
| <img src="https://github.com/user-attachments/assets/225a5fcc-38ee-49db-8466-accd35046102" width="280" /> | <img src="https://github.com/user-attachments/assets/9b67c88c-b720-4836-91a2-ea774e793e79" width="280" /> | <img src="https://github.com/user-attachments/assets/4738267e-81f3-4d2f-b38d-918409aacb39" width="280" /> |

#### Confusion Matrix (SAD Performance)
While ZNCC and SSD achieved 100% accuracy, SAD showed sensitivity to intensity shifts:

#### Detection Results per Image
| Image File | Actual Coins (TP) | SSD/ZNCC False Positives | SAD False Positives | False Negatives |
| :--- | :---: | :---: | :---: | :---: |
| `mario-bonusarea-a.png` | 19 | 0 | 0 | 0 |
| `mario-bonusarea-b.png` | 17 | 0 | 0 | 0 |
| `mario-bonusarea-c.png` | 12 | 0 | 0 | 0 |
| `mario-bonusarea-d.png` | 18 | 0 | 0 | 0 |
| `mario-bonusarea-e.png` | 10 | 0 | 0 | 0 |
| `mario-bonusarea-f.png` | 20 | 0 | 0 | 0 |
| `mario-bonusarea-h.png` | 41 | 0 | 0 | 0 |
| `mario-bonusarea-i.png` | 52 | **0** | **94** | 0 |
| `mario-bonusarea-j.png` | 19 | 0 | 0 | 0 |
| `mario-bonusarea-k.png` | 52 | **0** | **94** | 0 |


### Metric Comparision Summary
| Metric | Recall | Precision | F1-Score | Robustness |
| :--- | :---: | :---: | :---: | :---: |
| ZNCC | 100% | 100% | 1 | Superior |
| SSD | 100% | 100% | 1 | High |
| SAD | 100% | 58% | 0.73 | MODERATE - Sensitive to intensity shifts |

> * **Precision & Recall:** My implementation achieved **100% Recall** across all maps (all coins detected). 
> * **SAD Limitations:** In scenarios `i` and `k`, SAD's sensitivity to intensity changes led to 94 False Positives per image. 
> * **ZNCC/SSD Superiority:** Both achieved **100% Precision**, proving that precise template cropping and normalized metrics effectively filter out complex background noise.





