# CAD folder documentation

## Overview

This repository contains a variety of CAD drawings and 3D models in multiple formats. The files are organized into the following folders:

## Folder descriptions

### `STEP_full_assemblies`

This folder includes STEP files that represent the complete design or construction tree.

- **STEP files:** these files are compatible with various CAD programs, including SolidWorks, Catia, and AutoCAD. They adhere to the STEP (Standard for the Exchange of Product Data) format, which uses ASCII text to describe three-dimensional objects and models according to the ISO 10303 specification.

- **Usage:** use these files to restore and view full designs or construction assemblies in your preferred CAD software.

### `SW17_full_project`

This folder contains a complete project package, including all components, fasteners, printed circuit boards, and other parts, exemplified through a disinfection robot project.

**💡MMP - stands for Multipurpose Mobile Platform**

- **File compatibility:** these files are designed for SolidWorks version 2017 or newer.

- **Contents:** this comprehensive package includes all necessary components and models, providing a full representation of the project.

- **Folder Naming:** the main archive is named `MMP.00.00.00.000_Multipurpose_mobile_platform`. After extracting all the files into a single folder named `MMP.00.00.00.000_Multipurpose_mobile_platform`, locate the file with all zeros in the name, `MMP.00.00.00.000`, to open the full project.

### `Production_files`

This folder provides production-ready files in various formats that can be used to order parts without requiring specialized software.

- **File formats:** PDF, DXF, SLDDRW, and SLDPRT.

- **Usage:** these files contain detailed drawings and specifications sufficient for ordering parts directly from production facilities.

## File handling instructions

Due to GitHub's file size limitations (files larger than 25 MB are split), the files in this repository are divided into parts. To avoid issues when opening the packages:

1. **Download archives:** download all parts of the archive for each package.
2. **Extract files:** extract the downloaded archives into a single folder.

**Note:** ensure all parts are extracted together in the same directory to maintain file structure integrity.

## Accessing and using projects

- **Full projects:** for example, in the `SW17_full_project` folder, use the file named `MMP.00.00.00.000` to open the full project in SolidWorks. 

- **Editing and improvements:** after opening the project, you can rename assemblies, edit, or improve the models. We encourage you to suggest improvements or report issues to the project.

## ⚠️Important notice for the sheet metal parts

Sheet metal parts are subject to production variations. The current designs are based on the following coefficients and radii:

- **Coefficient (K):** 0.47
- **Sheet metal specifications:**
  - **0.8 mm Sheet:** Radius (R) = 1.2
  - **1.2 mm Sheet:** Radius (R) = 1.5
  - **2.0 mm Sheet:** Radius (R) = 2.4

### Post-production

- Parts may be painted after bending.
- Riveting nuts can be installed before painting if the threaded part is protected from the coating.
- Screws installed without lock washers should be secured with a thread lock (e.g., Loxeal 55-03).

### 📜Bill of Materials (BOM) and list of assemblies, drawings, original parts 
Comprehensive list of all assemblies and their corresponding files in the [BOM repository](https://github.com/openAMRobot/OpenAMR/tree/main/docs/hardware/BOM). It also includes details on sheet metal parts, fasteners, technological operations, and origin components.

**Note:** All components are highly interconnected and their functionality is dependent on one another.

## Contributing

If you wish to contribute to the project:

- **Issue reporting:** use the [ISSUE_TEMPLATE.md](https://github.com/openAMRobot/.github/blob/main/ISSUE_TEMPLATE.md) for reporting issues.
- **Submitting pull requests:** use the [PULL_REQUEST_TEMPLATE.md](https://github.com/openAMRobot/.github/blob/main/PULL_REQUEST_TEMPLATE.md) for submitting improvements or changes.
- **Contributing guidelines:** please read the [CONTRIBUTING.md](https://github.com/openAMRobot/OpenAMR/blob/main/CONTRIBUTING.md) for detailed contribution guidelines.

For further assistance, please refer to the repository’s main documentation or contact the repository maintainers.
