# 🖼️ Banner quality assessment system - Multi-model Deep Learning
## 📝 Introduction
This project focuses on researching and developing an automated system for evaluating the quality of advertising banners/posters based on Deep Learning architecture. Instead of relying on subjective perception, the system quantifies evaluation criteria such as aesthetics, readability, and contrast to provide an objective quality score, assisting designers and businesses in optimizing content before publication.

**Executing member**
- Huỳnh Phát Đạt - ISE-UIT
- Bùi Quốc Bảo - ISE-UIT
- Lê Minh Khôi - ISE-UIT

## 📖 Data

- [AdImageNet](https://huggingface.co/datasets/PeterBrendan/AdImageNet?utm_source=chatgpt.com): Banner image dataset published by author Peter Brendan.
- Experimental Data: Our team extracted and assigned labels to 4502 banner samples.
- Labeling Process: Labels were manually assigned on a scale from 0 to 5 based on guidelines from graphic design experts. To ensure reliability, the team performed statistical tests on a representative sample of 500 samples against the expert's labels.


## 🛠️ System Architecture
The system is designed using a multi-model framework, combining three advanced architectures to evaluate three core criteria:

### 1. Aesthetic Evaluation Model
- Architecture: Uses a pre-trained CLIP (Vision Transformer) model as the feature extractor (Backbone).
- Mechanism: Feature vectors from the CLIP are fed into an MLP (Regression Head) network to predict aesthetic scores.

### 2. Readability Evaluation Model
- Architecture: Uses ConvNeXt v2 (version convnextv2_tiny).
- Mechanism: Focuses on the ability to extract features of text on banners through MBConv blocks and Global Response Normalization (GRN).

### 3. Contrast Evaluation Model
- Architecture: Based on EfficientNet-B0.
- Mechanism: Utilizes Compound Scaling and MBConv blocks to identify color intensity differences between the main object and the background.

## 📊 Experiment
1. Label Reliability Testing 
- We used statistical methods to demonstrate that self-assigned labels are equivalent to expert labels: 
    - Paired t-test: The p-value for all three criteria is > 0.05, indicating no significant difference between the two sets of labels.
    - TOST (Two One-Sided Tests): Confirms high homogeneity when all criteria reach equivalence with a threshold of epsilon = 0.1.

| Criteria     | Mean diff | Paired t-test | TOST p-value<br>(lower) | TOST p-value<br>(upper) | TOST<br>(ε = 0.1) |
|--------------|:---------:|:-------------:|:--------------------:|:--------------------:|:--------------:|
| Aesthetic    | −0.006    | *p* = 0.75    | 3.43e-07             | 1.22e-08             | Equivalent     |
| Readability  | −0.029    | *p* = 0.27    | 7.00e-03             | 1.40e-06             | Equivalent     |
| Contrast     | −0.013    | *p* = 0.44    | 6.32e-07             | 1.24e-10             | Equivalent     |

### 2. Model Results
Performance of the models on the test set (scale 1-5):
| Metric | Aesthetic<br>ViT-B/32 | Readability<br>ConvNeXt-V2 | Contrast<br>EfficientNet-B0 |
|--------|:---------------------:|:--------------------------:|:---------------------------:|
| MAE    | 0.4132                | 0.4433                     | 0.4007                      |
| MSE    | 0.2628                | 0.3137                     | 0.2667                      |
| R2     | 0.3692                | 0.2481                     | 0.3243                      |


### 3. Overall Assessment
- Accuracy: The MAE score is approximately 0.40, indicating an average error of only about 0.4 points on a 5-point scale, demonstrating its ability to predict closely with human perception.
- Limitations: The R2 coefficient is still low due to the small data size and the sensitivity of collective perception (natural variation in human evaluation).

## 🚀 Conclusion & Future Development
### 1. Conclusion
- The team successfully built a multi-dimensional evaluation system, automating the banner quality control process on a large scale.
- The flexible combination of three distinct models optimizes each specific task, delivering highly practical results for designers.

### 2. Future Development
- Data Improvement: Hire more experts to expand the label set and cover more modern design styles.
- Technical Optimization: Research Multi-task Learning architecture (Unified Backbone) to run three prediction branches simultaneously, reducing model size and increasing processing speed.
- Adding Criteria: Add evaluation models for composition and color harmony.