# E57 Validator for Archivematica

This repository provides a script that uses the official [E57 Validator](http://www.libe57.org/download.html) tool to validate ASTM E57 files in [Archivematica](https://www.archivematica.org/).

## Installation

To install this script, follow these steps:

### 1. Download the official E57 validator tool

- Download the latest release for Windows x86 (64bit) of the [E57 validator](http://www.libe57.org/download.html) and put the `./bin/e57validate.exe` in the `/usr/share/` folder.

### 2. Install Wine

- Install [Wine](https://www.winehq.org/) e. g. by entering the commands in the terminal: `sudo apt install wine64`.

### 3. Create a new format policy tool

- In the Archivematica frontend, navigate to **Preservation planning** > **Format policy registry** > **Tools** > **Create new tool** or go directly to [this link](http://10.10.10.20/fpr/fptool/create/).
- Enter the following parameters:
  - **Description**: Enter `e57validate`.
  - **Version**: Enter the version you downloaded, e. g. `1.1.312`.
- Click **Save**.

### 4. Create a new validation command

- In the Archivematica frontend, navigate to **Preservation planning** > **Validation** > **Commands** > **Create new command** or go directly to [this link](http://10.10.10.20/fpr/fpcommand/create/).
- Fill in the following fields:
  - **The related tool**: Select **e57validate**.
  - **Description**: Enter `Validate using e57validate`.
  - **Command**: Paste the entire content of the [**e57-validator.py**](./src/e57-validator.py) file.
  - **Script type**: Select **Python script**.
  - **Command usage**: Select **Validation**.
  - Leave all other input fields and combo boxes untouched.
- Click **Save**.

### 5. Create a new validation rule for E57

- In the Archivematica frontend, navigate to **Preservation planning** > **Validation** > **Rules** > **Create new rule** or go directly to [this link](http://10.10.10.20/fpr/fprule/create/).
- Fill in the following fields:
  - **Purpose**: Select **Validation**.
  - **The related format**: Select **Image (Vector): ASTM E57 3D File Format: E57 3D File Format (fmt/643)**.
  - **Command**: Select **Validate using e57validate**.
- Click **Save**.

## Test

To test this validator, you can use the sample E57 files located [here](https://github.com/JoergHeseler/point-cloud-samples-for-preservation-testing/tree/main/E57).

### In Archivematica:

You can view the error codes and detailed validation results in the Archivmatica frontend after starting a transfer by expanding the `▸ Microservice: Validation` section and clicking on the gear icon of `Job: Validate formats`.

Files with no errors end with `valid` in their name and should pass validation with this script (i. e. return error code **0**). However, all other files contain errors and should fail validation (i. e. return error code **1**).

### In the command line:

You can use the validator at the command line prompt by typing `python e57-validator.py <E57 file to validate>`. You may also want to add `--validator-path=<path to the official e57validate>`.

## Dependencies

[Archivematica 1.13.2](https://github.com/artefactual/archivematica/releases/tag/v1.13.2) and the [E57 Validator 1.1.312](http://www.libe57.org/download.html) were used to analyze, design, develop and test this script.

## Background

As part of the [NFDI4Culture](https://nfdi4culture.de/) initiative, efforts are underway to enhance the capabilities of open-source digital preservation software like Archivematica to identify, validate and preserve 3D file formats. This repository provides a script to enable Graphics Language Transmission Format (E57) file validation in Archivematica, which is not supported by default in version 1.13.2, enhancing its 3D content preservation capabilities.

## Related projects

- [DAE Validator for Archivematica](https://github.com/JoergHeseler/dae-validator-for-archivematica)
- [glTF Metadata Extractor for Archivematica](https://github.com/JoergHeseler/gltf-metadata-extractor-for-archivematica)
- [Mesh Samples for Preservation Testing](https://github.com/JoergHeseler/mesh-samples-for-preservation-testing)
- [Point Cloud Samples for Digital Preservation Testing](https://github.com/JoergHeseler/point-cloud-samples-for-preservation-testing)
- [Siegfried Falls Back on Fido Identifier for Archivematica](https://github.com/JoergHeseler/siegfried-falls-back-on-fido-identifier-for-archivematica)
- [STL Cleaner](https://github.com/JoergHeseler/stl-cleaner)
- [STL Metadata Extractor for Archivematica](https://github.com/JoergHeseler/stl-metadata-extractor-for-archivematica)
- [STL Validator for Archivematica](https://github.com/JoergHeseler/stl-validator-for-archivematica)
- [X3D Validator for Archivematica](https://github.com/JoergHeseler/x3d-validator-for-archivematica)

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## Acknowledgments

Special thanks to the colleagues from the SLUB Dresden, specifically from the Infrastructure and Long-Term Availability division, for their support and valuable feedback during the development.

## Imprint

[NFDI4Culture](https://nfdi4culture.de/) – Consortium for Research Data on Material and Immaterial Cultural Heritage.  
Funded by the German Research Foundation (DFG), Project No. [441958017](https://gepris.dfg.de/gepris/projekt/441958017).

**Author**: [Jörg Heseler](https://orcid.org/0000-0002-1497-627X)  
**License**: [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)
