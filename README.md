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


Dataset Coverage Summary
=========================

Location             | # of Cameras | # of Boxes | Box Resolution(avg)
---------------------|--------------|------------|----------------
Sharif University    | 2            | 1,124      |    311x678
Local Shop Center    | 1            |   70       |    158x329
Local Hospital       | 1            |   591      |    145x280
Total                | 4            | 1,785      | 208x442 (all boxes)
