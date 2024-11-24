# Font Management Guide

This guide provides instructions for downloading, extracting, and installing fonts from Google Fonts.

## Steps to Manage Fonts

1. **Search and Download Fonts**
   - Visit [Google Fonts](https://fonts.google.com/).
   - Search for the desired fonts.
   - Download the selected fonts as a `.zip` file.  
     Example: `Arimo,Bitter,Edu_AU_VIC_WA_NT_Pre,Fira_Sans,IBM_Plex_Sans,etc.zip`.

2. **Extract the Font Files**
   - Unzip the downloaded file (`Arimo,Bitter,Edu_AU_VIC_WA_NT_Pre,Fira_Sans,IBM_Plex_Sans,etc.zip`) to a folder of your choice.  
     Example: `source_folder_path`.

3. **Extract `.ttf` Files**
   - Use the following command in Command Prompt (DOS) to copy all `.ttf` files from the extracted folders to a destination folder:
     ```dos
     for /r "source_folder_path" %f in (*.ttf) do @copy "%f" "destination_folder_path" /y
     ```
     Replace `source_folder_path` and `destination_folder_path` with the respective source and target directory paths.

4. **Install Fonts**
   - Navigate to the `destination_folder_path` where the `.ttf` files are located.
   - Double-click the desired `.ttf` files and click the **Install** button to add them to your operating system.

## Notes
- Ensure you have the necessary permissions to install fonts on your operating system.
- Use a font manager or system settings for bulk font installation if required.
