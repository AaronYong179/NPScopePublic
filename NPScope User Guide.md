<!---
@author: AaronYong179
@email: aaronyong7922@gmail.com; aaronyong@pathnova.com
--->

# NPScope User Guide

## Quick Start

1) Switch on the camera and ensure that sample details are entered on the relevant [Google Sheets](#Google-Sheets).
2) Start the NPScope desktop application by double-clicking on `NPScope_v4` on the `Desktop`.
3) Select the correct Sample Type and ID then click `Confirm sample details`. You should see a confirmation message being logged in the `Events Log`.
4) Click `Live` to start live imaging, `Snap` to capture the desired frame, and `Save` to save the image.


## Widgets
### Settings Menu
![Figure 1](https://drive.google.com/uc?export=view&id=1qTmxGxSTu6D6TYuqCXuHfwcgYYf7KS9W)
- **Set Output Path**
    - Sets the output path for all images saved by NPScope. By default, images will be saved in a folder called `NPScopeOutput` in the [Synology FileStation](#Synology-FileStation).
    - Select the relevant parent folder on Synology. For example, a sample for the 20k study should be placed within the folder titled `EBV20k`.
    - For example, the default folder structure would be:
        ```
        ./NPScopeOutput/
            230101/
                230101-CTL-0000-01.tif
                230101-CTL-0000-02.tif
                .
                .
                .
        ```
    - Changing the output folder via `Set Output Path` to "MyCustomFolder" only changes the parent folder:
        ```
        ./MyCustomFolder/
            230101/
                230101-CTL-0000-01.tif
                230101-CTL-0000-02.tif
                .
                .
                .
        ```
    - Note therefore that the date-based naming (`YYMMDD`) of the nested folders is forced. This is to ensure compatibility with the auto image analysis pipeline (_still in development_).

- **Reset Camera**
    - Rescans for and reinitialises the camera.
    - In previous versions of NPScope, a camera-bound error would require a hard restart of the entire app. In this version, simply click `Reset Camera` and wait for a notification to appear.
    - If an error notification appears, simply restart the camera and try again.
    
    ![Figure 2](https://drive.google.com/uc?export=view&id=1Y0HOT_fPhshXNVcc7MkGUAmB9FZRdwnW)
    - Otherwise, a success notification will appear. Simply click `OK` and use NPScope as usual.
    
    ![Figure 3](https://drive.google.com/uc?export=view&id=1onVE3-1mEHPISVhebf_KQ-evcjqvznGZ)

### Input sample details
![Figure 4](https://drive.google.com/uc?export=view&id=1_9R7NxpD0J-7Ln4egbNzJhSoq4LcmDgv)
- **Sample Type**
    - Choose the appropriate sample type. There are only two values: `Control` or `Patient`
- **Sample ID**
    - Choose the appropriate sample ID. These values will depend on the sample type selected.
    - `Control` samples will allow for sample IDs of `0000`, `0010`, `0040`, `0160`, or `0640`.
    - `Patient` samples will pull sample IDs from the specified [Google Sheets](#Google-Sheets).
    - For `Patient` samples, the Pathnova ID will be displayed first, followed by the [UID](#Google-Sheets) in brackets.


- **Confirm sample details**
    - Click this button to confirm the details entered under `Sample Type` and `Sample ID`.
    - A confirmation message will be logged on the `Events Log` widget. Verify that the sample details are correct before proceeding with image acquisition.


### Main Workflow
![Figure5](https://drive.google.com/uc?export=view&id=1ssDMU1ZHW5G7_QzuO30yU6yoElNRXGEg)
- **Live/Snap/Save**
    - These buttons are at the core of the NPScope workflow, and should be familiar to users of previous versions. 
    - The `Live` button is first clicked to start live imaging. Once a representative image is observed, `Snap` is clicked to freeze the display and prepare the image for writing. `Save` simply saves the image file accordingly.
    - These buttons are no longer deactivated to enforce a rigid workflow. The exception to this is the `Save` button, which will not be activated unless `Snap` is clicked first.
    - The `Save` button also displays a message on the `Events Log` widget. Verify that the [file name](#File-Naming) is correct.

### Events Log
![Figure6](https://drive.google.com/uc?export=view&id=1lWbvKmyOHjpE8s27W05HP0ZwlXC2ctMu)
- **Scrollable Textbox (unnamed)**
    - Displays confirmation and file saving messages.

---
## Addendum
### File Naming
- Sample details are automatically reformatted to fit into the following file naming system:
`<YYMMDDD>-<sample_type>-<UID>-<image_num>.tif`
- The field `<sample_type>` can take on the value `CTL` or `PAT`, referring to a control or patient sample respectively.
- The field `<UID>` refers to the unique identifier assigned to each control/patient sample. For controls, the UID will take on values `0000`, `0010`, `0040`, `0160`, or `0640`. For patient samples, the UID will be pulled from the specified [Google Sheets](#Google-Sheets).

### Google Sheets

#### Data Pulldown
- Exact details of which patient data to pulldown are not handled by me. Please ask Ben for more information or if there are any issues with pulling patient data from Google Sheets.
- As of _16 January 2023_, here are the details that are relevant to users of NPScope: **only rows with the current testing date will be pulled down**. In other words, data will only be pulled from entries where the `Date Tested` column indicates today's date.

#### UID
- Patient samples are identified by a four-character unique identifier (UID). This UID will be the last four characters of the patient's NRIC if given. Otherwise, the UID will be a [base26](https://www.translatorscafe.com/unit-converter/en-US/numbers/3-29/decimal-base-26/) representation of the decimal number given to the patient (e.g., the running integer code used by NUH: `NU124` or `NU20000`)
- The UID generation is handled on the Google Sheet's side (`UID List`) and NPScope simply pulls the relevant data down. 



### Synology FileStation
- In order to facilitate image analysis, images are automatically saved into a shared Synology FileStation.
- The default location is `/PN-slides/slides` on Synology.


---
## Patch Notes
#### 4.0.00
- NPScope migrated from Python 2.7 to Python 3.10.4
- Micro-Manager upgraded from 1.4 to 2.0.
- NPScope massively refactored to use OOP instead of floating functions and global variable declarations.
- Camera interface abstracted into a separate module to enable resetting it without restarting NPScope.
- Complications with threading completely removed. The GUI is now single-threaded. Python bindings to Micro-Manager operates on a separate thread but this is automatically handled by [pymmcore](https://github.com/micro-manager/pymmcore).
- Added ability to pulldown data from Google Sheets.
- New file naming system enforced.
- Events log added for logging sample detail confirmation and image writing events.
- **NOTE:** Image acquisition and display remain untouched. There should (theoretically) be no difference in image capturing with previous versions.


#### 4.0.01
- Brian raised an incorrect default file save location (previously in the same working directory as `NPScopeApp.py`). This is now changed to the Synology FileStation.
- Error handling added for when users try to start live imaging although the camera failed to initialise.
- Error handling added for when users try to snap an image although the camera failed to initialise.
- Error handling added for when no data is selected on Google Sheets (i.e. `UID List` is empty).
- Outstanding issues: proper closing of the NPScopeApp to be implemented: right now `Tkinter` is in charge of closing all outstanding tasks. 