# Cortado

<img width="64" src="src/frontend/src/assets/icons/png/64x64.png" alt="Cortado Logo"/>

**Cortado is a process mining tool dedicated for interactive/incremental process discovery.**

## Overview Functionality

- Import event logs `.xes` and initial process models `.ptml`
- Visually explore event logs with the variant explorer
- Discover initial process models from user-selected process behavior
- Incrementally extend process models by user-selected process behavior
- Manually edit process models under construction any time
- Export discovered process models as `.ptml` or `.pnml` files
- Temporal performance analysis, both model-based and model-independent


**Standalone builds** for **Windows 10/11**, **Linux**, and **macOS** (Apple Silicon only) are available from the GitHub Release Page.

## Demo

https://github.com/cortado-tool/cortado/assets/61526398/0b5b348a-c708-4049-8eea-81c5fc5feecb


## Repository Structure 

* `src/` contains the source code of Cortado
  * `src/backend` contains Cortado's Python-based backend 
  * `src/frontend` contains Cortado's frontend that is based on web technologies , i.e., an [Angular](https://angular.io/) web application embedded in an executable with [Electron](https://www.electronjs.org/)
* `build_scripts/` contains scripts to build the standalone executables for the three major operating systems: Windows, Linux, and macOS. (Please make sure to correctly follow the Setup instructions before executing the build scripts.)
* `LICENSE.txt`
* `README.md`
* `CHANGELOG.md` contains a history of Cortado releases 


## Setup
### Install Frontend Dependencies
* Install Node.js latest LTS Version: 18.13.0 (https://nodejs.org/en/download/)
* Install all packages required by the frontend
  * **Navigate to `src/frontend/`** 
  * **Execute `npm install`** (this command installs all dependencies listed in `src/frontend/package.json`)\
    _When building Cortado as a standalone application, we want to ensure that the application bundle only includes required dependencies. 
    As Angular dependencies are bundled via webpack, we do not want to include them. Hence, dependencies that are only used in the Angular codebase should be included under the `devDependencies` keyword in the `package.json`-file. All dependencies that are used in the Electron codebase must be included under the `dependencies` keyword.)_
### Install Backend Dependencies
* Install Python 3.10.x (https://www.python.org/downloads/). Make sure to install a 64-BIT version.
* Optional (recommended): Install Graphviz (required by PM4Py) and add it to your PATH, see https://graphviz.org/download/ and https://pm4py.fit.fraunhofer.de/static/assets/api/2.3.0/install.html
* Optional (recommended): Create a virtual environment (https://docs.python.org/3/library/venv.html) and activate it
* Install all packages required by the backend
  * Navigate to `src/backend/` 
  * Execute `pip install -r requirements.txt`

## Execute Cortado from Code
### Start Backend
* Navigate to `src/backend/`
* Execute `python main.py`
* For dynamic reloading of source code files, set environment variable `CORTADO_DEBUG` to `1`
### Start Frontend 
* In a Web-Browser
  * Navigate to `src/frontend/`
  * Execute `npm start` to build & run Cortado's frontend
  * Open your browser on http://localhost:4444/
* In a dedicated Window of the Current OS
  * Navigate to `src/frontend/`
  * Execute `npm start` to build & run Cortado's frontend
  * Execute `npm run electron-live-reload` that starts a window with Cortado


## Build Cortado&mdash;Standalone Application

To build executables from the source code, both the backend and frontend have to be converted.
We use PyInstaller (https://pyinstaller.org/) to bundle all backend related files into a single executable.
We use Electron (https://www.electronjs.org/) to generate an executable  of the Frontend. 

In `build_scripts/` there are scripts for each major OS to build Cortado.
* Windows `build_scripts/build_cortado_windows.ps1`
* MacOS `build_scripts/build_cortado_macos.sh`
* Linux `build_scripts/build_cortado_linux.sh`

Note that the operating system must match the script, otherwise the build will fail. 
Thus, if you are building Cortado for Windows, you must run the corresponding script on a Windows machine.

After the successful execution of the build script, the build is located in `src/frontend/`

## Contributing

### Linting and Code Quality

To maintain consistent code quality and formatting crucial, we have integrated Github Workflows along with npm scripts for linting and manual fixing of formatting errors.

#### Github Workflow

Our Github Workflow plays a pivotal role in ensuring code quality. Whenever changes are pushed to the repository, the workflow automatically triggers linting checks using various tools. We have separate jobs within the workflow to handle TypeScript, HTML, and SASS linting, as well as Python code formatting checks. If any issues are detected, the workflow provides prompt feedback, helping contributors address the problems early in the development cycle.

#### npm Scripts

In addition to the automated workflow, we have set up npm scripts that facilitate local development and manual checks for formatting errors.

- To perform comprehensive linting across TypeScript, HTML, and SASS files, use: `npm run lint`

- If linting issues are detected, you can initiate automatic fixes for TypeScript and SASS files using: `npm run lint-scripts-fix` and `npm run lint-styles-fix`

- For HTML files, you can manually review and fix the issues identified by the linter.

- We also support Python code formatting checks using the command: `black --check .`

These tools and scripts are designed to streamline the development process, ensuring that our codebase remains clean, consistent, and of high quality. Before submitting your contributions, make sure to run these checks locally and address any issues to facilitate smoother code reviews and integration.

## Relevant Publications for Cortado

| Publication                                                                                                                        | Authors                                                             | Year |
| ---------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- | ---- |
| [Defining and visualizing process execution variants from partially ordered event data](https://doi.org/10.1016/j.ins.2023.119958) | Schuster, D., Zerbato, F., van Zelst, S.J., van der Aalst, W.M.P.   | 2024 |
| [Incremental Discovery of Process Models Using Trace Fragments](https://doi.org/10.1007/978-3-031-41620-0_4)                       | Schuster, D., Föcking, N., van Zelst, S.J., van der Aalst, W.M.P.   | 2023 |
| [Mining Frequent Infix Patterns from Concurrency-Aware Process Execution Variant](https://doi.org/10.14778/3603581.3603603)        | Martini, M., Schuster, D., Wil M. P. van der Aalst                  | 2023 |
| [Cortado: A dedicated process mining tool for interactive process discovery](https://doi.org/10.1016/j.softx.2023.101373)          | Schuster, D., van Zelst, S.J., van der Aalst, W.M.P.                | 2023 |
| [Control-Flow-Based Querying of Process Executions from Partially Ordered Event Data](https://doi.org/10.1007/978-3-031-20984-0_2) | Schuster, D., Martini, M., van Zelst, S.J., van der Aalst, W.M.P.   | 2022 |
| [Conformance Checking for Trace Fragments Using Infix and Postfix Alignments](https://doi.org/10.1007/978-3-031-17834-4_18)        | Schuster, D., Föcking, N., van Zelst, S.J., van der Aalst, W.M.P.   | 2022 |
| [Temporal Performance Analysis for Block-Structured Process Models in Cortado](https://doi.org/10.1007/978-3-031-07481-3_13)       | Schuster, D., Schade, L., van Zelst, S.J., van der Aalst, W.M.P.    | 2022 |
| [A Generic Trace Ordering Framework for Incremental Process Discovery](https://doi.org/10.1007/978-3-031-01333-1_21)               | Schuster, D., Domnitsch, E., van Zelst, S.J., van der Aalst, W.M.P. | 2022 |
| [Freezing Sub-models During Incremental Process Discovery](https://doi.org/10.1007/978-3-030-89022-3_2)                            | Schuster, D., van Zelst, S.J., van der Aalst, W.M.P.                | 2021 |
| [Visualizing Trace Variants from Partially Ordered Event Data](https://doi.org/10.1007/978-3-030-98581-3_3)                        | Schuster, D., Schade, L., van Zelst, S.J., van der Aalst, W.M.P.    | 2021 |
| [Cortado—An Interactive Tool for Data-Driven Process Discovery and Modeling](https://doi.org/10.1007/978-3-030-76983-3_23)         | Schuster, D., van Zelst, S.J., van der Aalst, W.M.P.                | 2021 |
| [Incremental Discovery of Hierarchical Process Models](https://doi.org/10.1007/978-3-030-50316-1_25)                               | Schuster, D., van Zelst, S.J., van der Aalst, W.M.P.                | 2020 |

## Citing Cortado

If you are using or referencing Cortado in scientific work, please cite Cortado as follows.

> Schuster, D., van Zelst, S.J., van der Aalst, W.M.P. (2023). Cortado: A dedicated process mining tool for interactive process discovery. SoftwareX Vol. 22. Elsevier. https://doi.org/10.1016/j.softx.2023.101373.


Download citation 
https://www.sciencedirect.com/science/article/pii/S2352711023000699

DOI
[10.1016/j.softx.2023.101373](https://doi.org/10.1016/j.softx.2023.101373)



## Contact

If you are interested in Cortado, get in touch if you have any questions or custom request via Mail - [daniel.schuster@fit.fraunhofer.de](mailto:daniel.schuster@fit.fraunhofer.de)


