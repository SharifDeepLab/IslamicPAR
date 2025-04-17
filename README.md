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
The uploaded `dataset.xlsx` file in Drive provides annotations for the **Pedestrian Attribute Recognition (PAR)** task. This task is formulated as a **multi-label binary classification problem**, where each label is a binary attribute that the model must predict for each pedestrian image (box).

#### 📁 Columns Description:

- **`ID`**: Identifier for each pedestrian image (box), which corresponds to a file name in the dataset.
- **Binary Attribute Labels**:
  - **`U_color`**: Color of the **upper body clothing** [`U_black`, `U_blue`, `U_brown`, ...].
  - **`L_color`**: Color of the **lower body clothing** [`L_black`, `L_blue`, `L_brown`, ...].
  - **`Age_...`**: Attributes related to **age categories**.
  - **`Gender_female`**: Indicates whether the person is **female**.
  - **`Hair_...`**: Describes the **hair length**(only for men).
  - **`Upper_short`**: Indicates if the **sleeves are short** on the upper body(only for men).
  - **Accessories**:
    - **`Backpack`**
    - **`Bag`**
    - **`Hat`**
  - **`Jeans`**: Specifies if the lower body clothing is **jeans**.
  - **Islamic Region Attributes**:
    - **`Chador`**
    - **`Manto`**
    - **`Shawl`**
    - **`Maghnae`**
    - **`Roosari`**
  - **Clothing Style**:
    - **`Plaid`**
    - **`Stripped`**

- **`quality`**: This is **not a pedestrian attribute** but metadata indicating the **resolution quality** of the corresponding box (image).

#### 🧠 Selection Strategy:

To ensure both **diversity** and **balance** in the dataset, each pedestrian "tube" (a sequence of boxes for a person) undergoes a strategic selection:
- From each tube, we extract three candidate boxes:
  1. **Highest resolution**
  2. **Most typical (median) resolution**
  3. **Lowest resolution**
- Then, one of these is selected based on a combination of:
  - Dataset **generalization** goals (e.g., include occluded or varied illumination samples).
  - Dataset **balance** (e.g., ensuring both high- and low-resolution samples are included).

This strategy helps the model learn more **robust** and **generalizable** representations across varying conditions.
