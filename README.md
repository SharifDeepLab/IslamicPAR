# IslamicPAR
## Project Overview
This project focuses on Pedestrian Attribute Recognition (PAR), an important yet challenging task that plays a key role in Pedestrian Re-Identification (ReID) and Person Retrieval. We present a novel real-world dataset named **IslaminPAR** tailored to PAR's unique challenges in diverse environments and cultural contexts. We also fine-tune the C2T-Net model with some improvements to the dataset. We tackle challenges like:

1. **Cultural Adaptation**: Our dataset is specifically designed to reflect Islamic cultural norms, providing a unique contribution to the PAR community. This dataset includes a wide variety of clothing styles, such as Hijab models, and formal and informal wear for male and female pedestrians.
2. **Environmental & Scene Diversity**: To support robust model generalization, the dataset includes:
    - A range of illumination conditions (day/night, varying shadows)
    - Weather variations, including rainy conditions
    - Realistic challenges such as:
      - Occluded pedestrians
      - Multiple people per box
      - Partial body visibility

🛡️ **Privacy Considerations**
-------------------
To ensure ethical use and privacy, all faces have been blurred.

### 📊 Data Statistics
In the following table, information about the extracted boxes is reported.

Location             | # of Cameras | # of Boxes | Box Resolution(avg)
---------------------|--------------|------------|----------------
Sharif University    | 2            | 1,124      |    311x678
Local Shop Center    | 1            |   70       |    158x329
Local Hospital       | 1            |   591      |    145x280
Total                | 4            | 1,785      | 208x442 (all boxes)

### ⬇️ Download Dataset

You can download the full dataset from Google Drive:

🔗 [Download islamicPAR.zip](https://drive.google.com/your-download-link-here)

After extracting `islamicPAR.zip`, you should see the following structure:

```
islamicPAR/
├── release_data/
│   ├── c1_v1_01_05.jpg
│   ├── c2_v3_07_15.jpg
│   └── ...
└── dataset.xlsx
```

- **`release_data/`**: Contains all pedestrian image boxes (cropped from video).
- **`dataset.xlsx`**: Contains annotations for each image, including gender, clothing, accessories, and cultural attire.

---

### 🖼️ Image (Box) Description

The dataset contains 1,785 cropped pedestrian images (referred to as boxes), located in the release_data/ folder. Each box is extracted from a selected frame within a pedestrian trajectory (tube) captured in surveillance videos.

#### 📄 File Naming Format:

Each image filename follows the format:

```
cx_vx_number1_number2.jpg
```

Where:

- **`cx`** — Camera index (e.g., `c1`, `c2`, etc.)
- **`vx`** — Video sequence index recorded by the corresponding camera.
- **`number1`** — Tube index, identifying a unique pedestrian track within the video.
- **`number2`** — Selected frame index from that pedestrian tube.

#### 📌 Example:

```
c2_v3_07_15.jpg
```

This filename indicates:
- **Camera 2** (`c2`)
- **Video 3** recorded by Camera 2 (`v3`)
- **Tube 07**, representing one pedestrian's trajectory
- **Frame 15** selected from Tube 07

### 🧾 Label Description

The uploaded `dataset.xlsx` file provides annotations for each pedestrian image (box). This is a **multi-label binary classification** task, meaning each image may have multiple labels that are either true (1) or false (0).

#### 📁 Column Descriptions:

- **`ID`**: A unique identifier for each pedestrian image (box), corresponding to a file name in the dataset.

- **Binary Attribute Labels**:
  - **`U_color`**: Color of the **upper-body clothing** (e.g., `U_black`, `U_blue`, `U_brown`, ...).
  - **`L_color`**: Color of the **lower-body clothing** (e.g., `L_black`, `L_blue`, `L_brown`, ...).
  - **`Age_...`**: Attributes related to **age categories**.
  - **`Gender_female`**: Indicates whether the person is **female**.
  - **`Hair_...`**: Describes the **hair length** (for men).
  - **`Upper_short`**: Indicates whether the **sleeves are short** on the upper body (for men).
  - **Accessories**:
    - **`Backpack`**
    - **`Bag`**
    - **`Hat`**
  - **`Jeans`**: Indicates whether the lower-body clothing is **jeans**.
  - **Islamic Region Attributes** (for women):
    - **`Chador`**
    - **`Manto`**
    - **`Shawl`**
    - **`Maghnae`**
    - **`Roosari`**
  - **Clothing Style**:
    - **`Plaid`**
    - **`Stripped`**

- **`quality`**: A **metadata field**, not an attribute, indicating the **resolution quality** of the corresponding image (box).

> Note: `////U_Others////` and `////L_Others////` denote cases where the clothing color is not among the predefined categories or the body part is not visible.


### 🧠 Selection Strategy

To ensure both **diversity** and **balance** in the dataset, each pedestrian "tube" (i.e., a sequence of image boxes for a person) goes through a strategic selection process:

- Three candidate boxes are extracted per tube:
  1. One with the **highest resolution**
  2. One with the **median resolution**
  3. One with the **lowest resolution**

- One of these candidates is selected based on:
  - Dataset **generalization** objectives (e.g., including occluded or variably illuminated images).
  - Dataset **balance** considerations (e.g., incorporating both high- and low-resolution examples).

This strategy enables the model to learn more **robust** and **generalizable** features under a variety of visual conditions.

## Model Development
This section of the project includes our work of deploying and improving the model named Channel-Aware Cross-Fused Transformer-style Networks (C2T-Net) on the dataset. The C2T_Net achieved 1st place in the UPAR@WACV2024 challenge on the UPAR dataset in jan 2024. We fine-tuned the model using our data, and also tested and improved the model by using methods like 
1. Categorical loss: The loss that puts categorical labels in the categorical loss
2. Sample_weight: Adjust weights for loss using the distribution of positive and negative labels
3. Update logits: Update the predicted output using the recall of positive and negative labels
4. GradNorm: Learn weights for each attribute, plus the weights of the main model
5. Focal loss: Update the logits using the distribution of positive and negative labels.
Also, we used 3 types of fine-tuning for the base model
1. Full fine-tuning: Fine-tuning all weights of the model
2. Partial fine-tuning: 

