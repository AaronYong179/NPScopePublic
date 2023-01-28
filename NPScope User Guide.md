<!---
@author: AaronYong179
@email: aaronyong7922@gmail.com; aaronyong@pathnova.com
--->

# NPScope User Guide

## Quick Start

1) Switch on the camera and ensure that sample details are entered on the relevant [Google Sheets](#Google-Sheets).
2) Start the NPScope desktop application by double-clicking on `NPScope_v4` on the `Desktop`.
3) A filedialog will automatically appear. Select the relevant [parent folder](#Folder-Choice). You should see a confirmation message being logged in the `Events Log` 
4) Select the correct Sample Type and ID then click `Confirm sample details`. You should see a confirmation message being logged in the `Events Log`.
5) Click `Live` to start live imaging, `Snap` to capture the desired frame, and `Save` to save the image.
6) Keyboard shortcuts: 
    - `<F1>` for `Live`
    - `<F2>` for `Snap`
    - `<F3>` for `Save` 

<!-- https://drive.google.com/uc?export=view&id= -->


## Widgets
### Settings Menu
![Figure 1](https://drive.google.com/uc?export=view&id=1Dj-HT4VcbOvaNqJqMPsmuMXAoy2ch373)
- **Set Output Path**
    - Sets the output path for all images saved by NPScope.
    - A prompt to set the output path should already be given when NPScope starts. However, if an amendment is required, it can be done within this submenu.
    - Select the relevant parent folder on Synology. For example, images for the 20k study should be placed within the folder titled `EBV20k`. Read about this in more detail [here](#Folder-Choice).
    - The set output path will be logged on the `Events Log` widget. Verify that the location is correct before proceeding with image acquisition.

- **Reset Camera**
    - Rescans for and reinitialises the camera.
    - In previous versions of NPScope, a camera-bound error would require a hard restart of the entire app. In this version, simply click `Reset Camera` and wait for a notification to appear.
    - If an error notification appears, simply restart the camera and try again.
    
    ![Figure 2](https://drive.google.com/uc?export=view&id=1mK36oBGa9ilC71e3kA8Rf1MpmYiqkibM)
    - Otherwise, a success notification will appear. Simply click `OK` and use NPScope as usual.

    ![Figure 3](https://drive.google.com/uc?export=view&id=1aB_luxna2AEJ9_zK1puo9SsHnT-iD23F)

### Help Menu
- **User Guide**
    - Opens this user guide in the default web browser. The user guide will be updated alongside any changes made to NPScope, so please consult this guide if there are any queries.

    ![Figure 3.1](https://drive.google.com/uc?export=view&id=1wop5yNlRah2BPelKbJHdJdeMLAeU0O8C)

### Input sample details
![Figure 4](https://drive.google.com/uc?export=view&id=1yr3HpjRh3bv7QWTa0MgzOWerd398_oVa)
- **Sample Type**
    - Choose the appropriate sample type. There are only two values: `Control` or `Patient`.
- **Sample ID**
    - Choose the appropriate sample ID. These values will depend on the sample type selected.
    - `Control` samples will allow for sample IDs of `0000`, `0010`, `0040`, `0160`, or `0640`.
    - `Patient` samples will pull sample IDs from the specified [Google Sheets](#Google-Sheets).
    - For `Patient` samples, the Pathnova ID will be displayed first, followed by the [UID](#Google-Sheets) in brackets.


- **Confirm sample details**
    - Click this button to confirm the details entered under `Sample Type` and `Sample ID`.
    - A confirmation message will be logged on the `Events Log` widget. Verify that the sample details are correct before proceeding with image acquisition.

### Main Workflow
![Figure5](https://drive.google.com/uc?export=view&id=1EEPJPm8TJ8SjZPnIrNkK4grse1NxWtMp)
- **Live/Snap/Save**
    - These buttons are at the core of the NPScope workflow, and should be familiar to users of previous versions. 
    - The `Live` button is first clicked to start live imaging. Once a representative image is observed, `Snap` is clicked to freeze the display and prepare the image for writing. `Save` simply saves the image file accordingly.
    - These buttons are no longer deactivated to enforce a rigid workflow. The exception to this is the `Save` button, which will not be activated unless `Snap` is clicked first.
    - The `Save` button also displays a message on the `Events Log` widget. Verify that the [file name](#File-Naming) is correct.
    - Keyboard shortcuts are provided to help optimise workflow. `<F1>` maps to `Live`, `<F2>` maps to `Snap`, and `<F3>` maps to `Save`.

### Events Log
![Figure6](https://drive.google.com/uc?export=view&id=1t1Yb5_80oHgeZ7kCcKPdBjIh27iR6n8j)
- **Scrollable Textbox (unnamed)**
    - Displays output directory changes, confirmation, and file saving messages.

---
## Addendum
### File Naming
- Sample details are automatically reformatted to fit into the following file naming system:
`<YYMMDDD>-<sample_type>-<UID>-<image_num>.tif`
- The field `<sample_type>` can take on the value `CTL` or `PAT`, referring to a control or patient sample respectively.
- The field `<UID>` refers to the unique identifier assigned to each control/patient sample. For controls, the UID will take on values `0000`, `0010`, `0040`, `0160`, or `0640`. For patient samples, the UID will be pulled from the specified [Google Sheets](#Google-Sheets).

### Folder Choice
- In short, simply pick one of the following folders: `Clinical`, `EBV20k`, or `R&D`. A date-stamped folder will automatically be created within the user-selected folder.
- After selecting the correct folder, you should see a confirmation message being logged on the `Events Log`. Verify that the correct destination is set before proceeding.
- There should be **no need to manually create a date-stamped folder**.
- An example scenario:
    - The folder `Clinical` was selected by the user as the output path. Images are captured on the 1st of January 2023.
    - NPScope first automatically creates the folder `230101` within `Clinical` if it does not already exist.
    - NPScope will then automatically save images within the folder `230101`. An example of such a directory structure would be as follows:
    ```
        ./EBV20k/
            230101/
                230101-CTL-0000-01.tif
                230101-CTL-0000-02.tif
                .
                .
                .
    ```
- If a folder is not provided, NPScope will disable saving and an error message will appear.

![Figure5](https://drive.google.com/uc?export=view&id=1os5mQ3MkThDto31ad_j08YpCTxLZqeA4)

### Google Sheets

#### Data Pulldown
- Exact details of which patient data to pulldown are not handled by me. Please ask Ben for more information or if there are any issues with pulling patient data from Google Sheets.
- As of _16 January 2023_, here are the details that are relevant to users of NPScope: **only rows with the current testing date will be pulled down**. In other words, data will only be pulled from entries where the `Date Tested` column indicates today's date.

#### UID
- Patient samples are identified by a four-character unique identifier (UID). This UID will be the last four characters of the patient's NRIC if given. Otherwise, the UID will be a [base26](https://www.translatorscafe.com/unit-converter/en-US/numbers/3-29/decimal-base-26/) representation of the decimal number given to the patient (e.g., the running integer code used by NUH: `NU124` or `NU20000`)
- The UID generation is handled on the Google Sheet's side (`UID List`) and NPScope simply pulls the relevant data down. 

### Synology FileStation
- In order to facilitate image analysis, images are to be saved into a shared Synology FileStation.

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


#### 4.0.02
- NPScopeApp should close properly with no side effects now.
- This User Guide can now be opened from within NPScope.
- Ben raised an issue where NPScope would occasionally save images in the same directory as the `NPScopeApp.py` script.
    - Steps to recreate this issue: when opening the filedialog by clicking `Set Output Path`, the user might click "Cancel" instead of actually selecting any destination folder.
    - Tkinter's `filedialog.askdirectory` returns an [empty string if this occurs](https://stackoverflow.com/questions/15010461/askopenfilename-handling-cancel-on-dialogue). When joining an empty string with the date-stamped folder, `os.path.join` discards all invalid strings and [simply starts from the current working directory](https://docs.python.org/3/library/os.path.html#os.path.join). 
    - In other words, `os.path.join("", "230101")` would result in `./230101`.
    - Empty strings are now handled.
- Users would either save images in the default location (and fail to move them to the correct folders later) or manually create and name date-stamped folders, resulting in nested duplicates. A default location is now removed. Users must now consciously select a destination folder for image saving.
- The events log now updates when an output folder is selected.
- User Guide rewritten to make the point on automatic date-stamped folder creation more clear (hopefully).
- Camera settings are enforced via Micro-Manager upon every startup. More information on what led to this change will not be detailed here.