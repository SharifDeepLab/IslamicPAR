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

**Note**: The variations in box resolution across scenes, as well as among individual boxes, stem from our box selection strategy applied to each person's tube (i.e., the sequence of boxes corresponding to that person). For every tube, we first identify three representative boxes: one with the highest resolution, one with the most typical (median) resolution, and one with the lowest resolution. Then, from these three, we select a single box based on parameters aimed at both generalizing and balancing the dataset — such as prioritizing occluded or diversely illuminated boxes for generalization, and ensuring a mix of high- and low-resolution samples for balance

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

