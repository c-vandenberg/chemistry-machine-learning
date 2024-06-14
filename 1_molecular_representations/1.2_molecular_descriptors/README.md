# 1.2 Molecular Descriptors in Machine Learning Models

## 1.2.1 Introduction to Molecular Descriptors

Molecular descriptors are an **abstract representations of certain structural features of a molecule**. The majority of molecular descriptors can be classified according to their **"dimensionality"**, which refers to the representation of molecules from which descriptor values are computed **<sup>1</sup>**. This includes:

1. **0D Molecular Descriptors**:
   * This is the simplest molecular representation and is independent of any knowledge concerning the molecular structure
   * Examples include atomic mass, atomic charge, covalent & VDW radii, atomic polarizability, electronegativities & hydrophobic atomic constants **<sup>2</sup>**
2. **1D Molecular Descriptors**:
   * This is a substructure list representation and consists of a list of **structural fragments** of a molecule
   * The list of fragments can be **functional groups**, **substituents of interest** or **fingerprints**. Therefore, complete knowledge of the molecules structure is not required **<sup>2</sup>**
   * A common approach is to **encode** this list of molecular fragments into a **bit string**, which encodes the **presence or absence of a certain structural fragment**. This is called a **1D molecular fingerprint** **<sup>3</sup>** 

        <br>
        <div align="center">
          <img src="https://github.com/c-vandenberg/chemistry-machine-learning/assets/60201356/f043aca7-a03b-42b3-803e-fac864c02d5e", alt="fragment-based-1d-fingerprint" width=500/>
          <p>
            <b>Fig 1</b> Fragment-based 1D molecular fingerprint
          </p>
        </div>
        <br>
   
   * The most popular 1D molecular fingerprint methods is the **Morgan Fingerprint** **<sup>4</sup>**, upon which the **extended-connectivity fingerprint (ECFP)**

3. **2D Molecular Descriptors**:
   * 2D molecular descriptors consider how the atoms are connected/define the molecular representation based on the connectivity of atoms
   * The most commonly used 2D molecular representation approach is a **simplified molecular-input line-entry system (SMILES) string** **<sup>5</sup>**
   * A SMILES string is linear notation that encodes connectivity, structural & geometric properties of a molecule

        <br>
        <div align="center">
          <img src="https://github.com/c-vandenberg/chemistry-machine-learning/assets/60201356/4928886a-0bf4-4a5f-9bc2-b1ea72b8617f", alt="smiles-string" width=500/>
          <p>
            <b>Fig 2</b> SMILES string for the antibiotic ciprofloxacin
          </p>
        </div>
        <br>

4. **3D Molecular Descriptors**:
   * 3D molecular descriptors define the molecular representation not only as the connectivity of the atoms, but also as the spatial configuration of the molecule **<sup>2</sup>**
   * A popular 3D descriptor approach is 3D pharmacophore-type representations where features (e.g. hydrophobic regions or hydrogen bond donors) known or thought to be responsible for biological activity are mapped to positions on the molecule **<sup>1</sup>**
   * Examples of 3D molecular descriptors include **WHIM** descriptors **<sup>6</sup>**, **EVA** **<sup>7</sup>** & **the EEVA** **<sup>8</sup>** descriptors, **3D-MoRSE** descriptors **<sup>9</sup>** and the **GETAWAY** **<sup>10</sup>** descriptors

## 1.2.2 Molecular Fingerprints

Fingerprint representations of molecular structure & properties are a particularly complex form of molecular descriptor. Fingerprints are typically **encoded as binary bit strings** that represent a **bit 'pattern'** characteristic of a given molecule. **<sup>1</sup>** 

Depending on what molecular descriptor (or molecular descriptors) the fingerprint is based on, what this bit 'pattern' represents will be different. For example, molecular fingerprints can be designed to account for fragment-based (1D) molecular descriptors, connectivity-based (2D) molecular descriptors, or spatial configuration-based (3D) molecular descriptors.

An example of a **binary molecular fingerprint** (also known as a **keyed-based molecular fingerprint**) model is shown below (taken from *Xue et al*). **<sup>2</sup>** In a binary/key-based molecular fingerprint, each bit accounts for the **absence** (i.e. "0") or **presence** (i.e. "1") of given structural or chemical properties. In this case, it is number of hydrogen-bonds, number of aromatic bonds & fraction of single non-ring bonds. These are then combined with a **32 bit MACCS key** structural key fragment, which defines the absence or presence of specific chemical substructures or patterns:

  <br>
  <div align="center">
    <img src="https://github.com/c-vandenberg/chemistry-machine-learning/assets/60201356/32e93ca7-55eb-4e8d-9fcb-e3804621faf3", alt="binary-molecular-fingerprint" width=500/>
    <p>
      <b>Fig 3</b> Schematic representation of a binary molecular fingerprint
    </p>
  </div>
  <br>

## 1.2.3 Key-Based Molecular Fingerprints - MACCS Keys

As mentioned in **Fig 3**, in keyed-based molecular fingerprints, each bit is associated with a **specific descriptor and value**, with each bit encoding for the absence or presence of a property. In this case, it is number of hydrogen bonds, number range of aromatic bonds, fraction of single non-ring bonds, and the absence or presence of specific fragments.

A widely used key-based molecular fingerprint is **Molecular ACCess System (MACCS) keys**. **<sup>11</sup>** The MACCS keys are a **set of structural keys** encoding for a set predefined substructures/fragments, with each bit indicating the absence or presence of a particular substructure/fragment. Many MACCS keys exist, **<sup>12</sup>** but the most commonly used are **166 and 960-bits long**, encoding 166 and 960 substructures/fragments respectively.

<br>
  <div align="center">
    <img src="https://github.com/c-vandenberg/chemistry-machine-learning/assets/60201356/6834d808-b1a8-487d-ab4f-a3b9a5c252b1", alt="maccs-keys" width=300/>
    <p>
      <b>Fig 4</b> MACCS keys example illustration
    </p>
  </div>
  <br>

## 1.2.4 Hash-Based Molecular Fingerprints - Daylight Fingerprint & ECFPs

However, widely used molecular fingerprints often consist of many more bit positions than the one shown in **Fig 3**. For example, in the **Daylight fingerprint** **<sup>13</sup>**, which was a milestone in the field in 1995, consists of 2,048 bits. 

Such complex molecular fingerprints are referred to as **hash-based molecular fingerprints**. These differ from key-based fingerprints in that each feature is generated from the molecule itself, whereas with key-based fingerprints the **patterns are pre-defined**. The length of the hashed-fingerprints can set prior to their generation, and a **hash function** maps molecular patterns (e.g. properties or structural patterns) to **non-unique/overlapping bit segments**, which usually produces very specific bit patterns. **<sup>14</sup>**

As a result, single bit positions can **no longer be associated with one specific feature** as they are in binary/keyed molecular fingerprints. **<sup>2</sup>**

The Daylight fingerprint **encodes for every connectivity pathway** within a molecule up to a given length **<sup>14</sup>**. There are also **circular hashed-based fingerprints**, whereby neighbouring atoms (usually heavy/non-hydrogen atoms) are encoded into **multiple circular layers up to a given diameter** (**Fig 5**).

  <br>
  <div align="center">
    <img src="https://github.com/c-vandenberg/chemistry-machine-learning/assets/60201356/a34d9bee-87a0-49de-b394-6e9926c4b73c", alt="ecfp_iterations" width=300/>
    <p>
      <b>Fig 5</b> Illustration of iterative circular identification and encoding of neighbouring atoms in ECFP circular fingerprints <b><sup>15</sup></p></b>
    </p>
  </div>

A widely used class of circular fingerprints are the **Extended Connectivity Fingerprints (ECFPs)** which are based on the aforementioned **Morgan algorithm**. **<sup>14</sup>**

### 1.2.2 The Importance of Molecular Fingerprints

Molecular fingerprints are a fundamental and versatile approach for representing chemical compounds in cheminformatics & computational chemistry. The reasons for this and the uses of molecular fingerprints are several-fold:

1. **Dimensionality Reduction**:
  * Chemical compounds can be highly complex. Molecular fingerprints condense this complexity into a binary or numerical format, **reducing the dimensionality of the data**
  * This makes is more feasible to compare, analyze, and model large chemical datasets

2. **Chemical Similarity**:
  * Molecular fingerprints are widely used for assessing the similarity between chemical compounds
  * By comparing the fingerprints of different molecules, structurallly similar compounds can be identified, which is crucial in lead compound identification & virtual screening

3. **Substructure Analysis**:
  * There is often a need for to identify specific substructures within molecules
  * Because molecular fingerprints can be designed to encode the presence of absence of predefined substructures or molecular fragments, this allows for efficient substructure searching

4. **Quantitative Structure-Activity Relationship (QSAR) Modelling**:
  * QSAR models aim to predict the biological or chemical activity of compounds based on their structural features
  * Molecular fingerprints, which capture & encode molecular structure, are key input variables for QSAR modelling

5. **Database Searching**:
  * Molecular fingerprints facilitate the **rapid searching of chemical databases**
  * By representing molecules as fingerprints, rapid querying of chemical databases is possible, allowing for quick identification of compounds with desired structural or functional characteristics

6. **Clustering & Diversity Analysis**:
  * Molecular fingerprints can be used to **group chemical compounds into clusters** based on structural similarities
  * This allows for efficient exploration of chemical space for identifying diverse compound sets and designing compound libraries

### 1.2.3 Molecular Fingerprints in Machine Learning

As stated in section 1.2.1, molecular fingerprints serve as a compact and informative representation of molecules, and are used extensively in applications ranging from similarity searching & clustering, to QSAR modeling and virtual screening in drug discovery.

In recent years, many of these applications have started to use sophisticated 3D structure-based fingerprints built from algebraic topology, differential geometry, geometric graph theory and algebraic graph theory. These molecular fingerprints are then paired with advanced machine learning (ML) algorithms **<sup>16</sup>** such as:
* **Random forest** (RF)
* **Gradient boosting decision tree** (GBDT)
* **Single-task deepneural networks** (ST-DNNs)
* **Multi-task deep neural networks** (MT-DNNs)
* **Convolutional neural network** (CNN)
* **Recurrent neural network** (RNN)

With the advancement of deep learning (DL) technology, the growth of drug-related data, and the proliferation of user-friendly DL frameworks in popular programming langauages, **<sup>17</sup>** **<sup>18</sup>** methodologies based on these ML algorithms are becoming more ubiquitous in all steps of the drug discovery & drug development process.

Data quality and data representation have a significant impact on the performance of ML-based predictive models as both heavily contribute to the quality of pre-training. Therefore, there has been a surge of interest in research on molecular representation  


## 1.2.4 References

**[1]** Xue, L. and Bajorath, J. (2000) ‘Molecular descriptors in Chemoinformatics, computational combinatorial chemistry, and virtual screening’, *Combinatorial Chemistry & High Throughput Screening*, 3(5), pp. 363–372. <br><br>
**[2]** Todeschini, R., Consonni, V. and Gramatica, P. (2009) ‘Chemometrics in Qsar’, *Comprehensive Chemometrics*, pp. 129–172. <br><br>
**[3]** Kim, J. *et al.* (2021) ‘Comprehensive survey of recent drug discovery using Deep Learning’, *International Journal of Molecular Sciences*, 22(18), p. 9983. <br><br>
**[4]** Morgan, H.L. (1965) ‘The generation of a unique machine description for chemical structures-a technique developed at Chemical Abstracts Service.’, *Journal of Chemical Documentation*, 5(2), pp. 107–113. <br><br>
**[5]** Weininger, D. (1988) ‘Smiles, a chemical language and information system. 1. introduction to methodology and encoding rules’, *Journal of Chemical Information and Computer Sciences*, 28(1), pp. 31–36. <br><br>
**[6]** Todeschini, R., Lasagni, M. and Marengo, E. (1994) ‘New molecular descriptors for 2D and 3D structures. theory’, *Journal of Chemometrics*, 8(4), pp. 263–272. <br><br>
**[7]** Ferguson, A.M. et al. (1997) ‘EVA: A new theoretically based molecular descriptor for use in QSAR/QSPR analysis’, *Journal of Computer-Aided Molecular Design*, 11(2), pp. 143–152. <br><br>
**[8]** Tuppurainen, K. (1999) ‘Eeva (Electronic Eigenvalue): A new QSAR/QSPR descriptor for electronic substituent effects based on molecular orbital energies’, *SAR and QSAR in Environmental Research*, 10(1), pp. 39–46. <br><br>
**[9]** Schuur, J.H., Selzer, P. and Gasteiger, J. (1996) ‘The coding of the three-dimensional structure of molecules by molecular transforms and its application to structure-spectra correlations and studies of biological activity’, *Journal of Chemical Information and Computer Sciences*, 36(2), pp. 334–344. <br><br>
**[10]** Consonni, V., Todeschini, R. and Pavan, M. (2002) ‘Structure/response correlations and similarity/diversity analysis by getaway descriptors. 1. theory of the novel 3D Molecular Descriptors’, *Journal of Chemical Information and Computer Sciences*, 42(3), pp. 682–692. <br><br>
**[11]** Dalke, A., *MACCS key 44*. Available at: http://www.dalkescientific.com/writings/diary/archive/2014/10/17/maccs_key_44.html (Accessed: 14 June 2024).<br><br>
**[12]** Durant, J.L. et al. (2002) ‘Reoptimization of MDL keys for use in Drug Discovery’, Journal of Chemical Information and Computer Sciences, 42(6), pp. 1273–1280.<br><br>
**[13]** James, C.A., Weininger, D. ‘Daylight theory manual’, *Daylight Chemical Information Systems, Inc.*, Irvine, CA, 1995. <br><br>
**[14}** David, L. et al. (2020) ‘Molecular representations in AI-Driven Drug Discovery: A review and practical guide’, *Journal of Cheminformatics*, 12(1).<br><br>
**[15}** Extended connectivity fingerprint ECFP - Extended Connectivity Fingerprint ECFP | Chemaxon Docs. Available at: https://docs.chemaxon.com/display/docs/fingerprints_extended-connectivity-fingerprint-ecfp.md (Accessed: 14 June 2024).<br><br>
**[16]** Gao, K. *et al.* (2020) ‘Are 2D fingerprints still valuable for drug discovery?’, *Physical Chemistry Chemical Physics*, 22(16), pp. 8373–8390.<br><br>
**[17]** Abadi, M. *et al.* (2015) ‘TensorFlow: Large-Scale Machine Learning on Heterogeneous Systems’, https://www.tensorflow.org/, Software available from tensorflow.org. <br><br>
**[18]** Paszke, A. *et al.* (2017) ‘NIPS Autodiff Workshop’.

