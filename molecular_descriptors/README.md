# 1 Molecular Descriptors/Representations in Machine Learning Models

## 1.1 Introduction to Molecular Descriptors

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
   
   * The most popular 1D molecular fingerprint methods is the **Morgan Fingerprint** **<sup>4</sup>**, also known as the **extended-connectivity fingerprint (ECFP4)**

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

## 1.2 Molecular Fingerprints

Fingerprint representations of molecular structure & properties are a particularly complex form of molecular descriptor. Fingerprints are typically **encoded as binary bit strings** that represent a **bit 'pattern'** characteristic of a given molecule. **<sup>1</sup>** 

Depending on what molecular descriptor (or molecular descriptors) the fingerprint is designed to account for, what this bit 'pattern' represents will be different. For example, molecular fingerprints can be designed to account for fragment-based (1D) molecular descriptors, connectivity-based (2D) molecular descriptors, or spatial configuration-based (3D) molecular descriptors.

An example of a **binary molecular fingerprint** model is shown below (taken from *Xue et al*). **<sup>2</sup>** In a binary molecular fingerprint, each bit accounts for the **presence** (i.e. "1") or **absence** (i.e. "0") of given structural or chemical properties. In this case, it is number of hydrogen-bonds, number of aromatic bonds & fraction of single non-ring bonds. These are then combined with a **32 bit MACCS key** structural key fragment, which defines the absence or presence of specific chemical substructures or patterns:

  <br>
  <div align="center">
    <img src="https://github.com/c-vandenberg/chemistry-machine-learning/assets/60201356/32e93ca7-55eb-4e8d-9fcb-e3804621faf3", alt="binary-molecular-fingerprint" width=500/>
    <p>
      <b>Fig 3</b> Schematic representation of a binary molecular fingerprint
    </p>
  </div>
  <br>

As mentioned in **Fig 3**, in **"keyed" molecular fingerprints**, each bit is associated with a **specific descriptor and value**. In this case, it is number of hydrogen bonds, number range of aromatic bonds, fraction of single non-ring bonds, and the absence or presence of specific fragments.

However, widely used molecular fingerprints often consist of many more bit positions than the one shown in **Fig 3**. For example, in the **Daylight fingerprint** **<sup>11</sup>**, which was a milestone in the field in 1995, consists of 2,048 bits. Such complex molecular fingerprints are often "hashed", meaning that properties or structural patterns are **mapped to overlapping bit segments**, which usually produces very specific bit patterns. As a result, single bit positions can **no longer be associated with one specific feature** as they are in binary/keyed molecular fingerprints. **<sup>2</sup>**

Hashing is a convenient approach when many structural paths or conformational states are being monitored.

## References

**[1]** Xue, L. and Bajorath, J. (2000) ‘Molecular descriptors in Chemoinformatics, computational combinatorial chemistry, and virtual screening’, *Combinatorial Chemistry & High Throughput Screening*, 3(5), pp. 363–372. <br><br>
**[2]** Todeschini, R., Consonni, V. and Gramatica, P. (2009) ‘Chemometrics in Qsar’, *Comprehensive Chemometrics*, pp. 129–172. <br><br>
**[3]** Kim, J. et al. (2021) ‘Comprehensive survey of recent drug discovery using Deep Learning’, *International Journal of Molecular Sciences*, 22(18), p. 9983. <br><br>
**[4]** Morgan, H.L. (1965) ‘The generation of a unique machine description for chemical structures-a technique developed at Chemical Abstracts Service.’, *Journal of Chemical Documentation*, 5(2), pp. 107–113. <br><br>
**[5]** Weininger, D. (1988) ‘Smiles, a chemical language and information system. 1. introduction to methodology and encoding rules’, *Journal of Chemical Information and Computer Sciences*, 28(1), pp. 31–36. <br><br>
**[6]** Todeschini, R., Lasagni, M. and Marengo, E. (1994) ‘New molecular descriptors for 2D and 3D structures. theory’, *Journal of Chemometrics*, 8(4), pp. 263–272. <br><br>
**[7]** Ferguson, A.M. et al. (1997) ‘EVA: A new theoretically based molecular descriptor for use in QSAR/QSPR analysis’, *Journal of Computer-Aided Molecular Design*, 11(2), pp. 143–152. <br><br>
**[8]** Tuppurainen, K. (1999) ‘Eeva (Electronic Eigenvalue): A new QSAR/QSPR descriptor for electronic substituent effects based on molecular orbital energies’, *SAR and QSAR in Environmental Research*, 10(1), pp. 39–46. <br><br>
**[9]** Schuur, J.H., Selzer, P. and Gasteiger, J. (1996) ‘The coding of the three-dimensional structure of molecules by molecular transforms and its application to structure-spectra correlations and studies of biological activity’, *Journal of Chemical Information and Computer Sciences*, 36(2), pp. 334–344. <br><br>
**[10]** Consonni, V., Todeschini, R. and Pavan, M. (2002) ‘Structure/response correlations and similarity/diversity analysis by getaway descriptors. 1. theory of the novel 3D Molecular Descriptors’, *Journal of Chemical Information and Computer Sciences*, 42(3), pp. 682–692. <br><br>
**[11]** James, C.A., Weininger, D. ‘Daylight theory manual’, *Daylight Chemical Information Systems, Inc.*, Irvine, CA, 1995. <br><br>
