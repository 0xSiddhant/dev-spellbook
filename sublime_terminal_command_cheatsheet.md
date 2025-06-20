# Sublime Text Terminal Command Use Cases

This document provides a list of practical use cases for the Sublime Text terminal command `subl`.

## Core `subl` Command

- **Use Case:** Simply opening Sublime Text without any specific file or folder.
`bash subl`

## Opening Files

- **Use Case 1: Opening a single file for quick editing.**
    
    `bash subl my_document.txt`
    
- **Use Case 2: Opening multiple files simultaneously.**
    
    `bash subl file1.py file2.js report.md`
    
- **Use Case 3: Opening a file at a specific line number (and optionally column).**
    
    `bash subl error_log.txt:150 subl code.cpp:23:5`
    

## Opening Folders

- **Use Case: Opening a project directory to work on all its files.**
    
    `bash subl my_project_folder`
    

## Creating New Files

- **Use Case: Quickly creating a new scratchpad file or starting a new document.**
    
    `bash subl new_file.txt`
    

## Modifying Existing Files

- **Use Case 1: Opening a file in the background (without activating the Sublime Text window).**
    
    `bash subl --background/-b notes.txt`
    
- **Use Case 2: Opening a file for editing and waiting for the file to be closed before the terminal command finishes (useful in scripts).**
    
    `bash subl --wait/-w config.ini echo "Configuration updated."`
    
- **Use Case 3: Opening a file in a new window.**
    
    `bash subl --new-window important_document.md`
    

## Working with Projects

- **Use Case: Opening a specific Sublime Text project file.**
    
    `bash subl my_project.sublime-project`
    

## Advanced Options

- **`-safe-mode`**: Starts Sublime Text in a clean state for troubleshooting.
`bash subl --safe-mode`
- **`-command <command>`**: Executes a specific Sublime Text command after the application starts (example: setting syntax).
`bash subl --command "set_file_type Python" new_script.py`
- **`-result-file <file>`**: With `-wait`, writes the closed file path to a specified file (for scripting).
`bash subl --wait input.txt --result-file output.txt`
- **`-stay` (macOS only)**: Keeps the `subl` process running in the background for faster subsequent commands.
`bash subl --stay`

## More Practical Use Cases

- **Quickly Reviewing Logs or Output:**`bash python my_script.py > output.log subl output.log`
- **Enhanced Log Review: Jumping to an error line.**`bash # (Assume your script outputs an error like "Error in file app.py:42") ./run_analysis.sh | grep "Error in file" | awk -F ':' '{print $2}' | xargs -I {} subl app.py:{}`
- **Scripting File Operations with Sublime Text:**`bash #!/bin/bash CONFIG_FILE="settings.ini" subl --wait "$CONFIG_FILE" echo "You have finished editing $CONFIG_FILE" # Add further actions based on the content of settings.ini`
- **Opening Specific Files from Search Results:**`bash grep -l "TODO:" ./*.py | xargs subl find . -name "*.test.js" | xargs subl`
- **Comparing File Versions Quickly (using a package like FileDiff):**`bash subl --command "file_diff {\"files\": [\"old_version.txt\", \"new_version.txt\"]}"`
- **Opening a Project in a New Window for Focused Work:**`bash subl --new-window another_project.sublime-project`
- **Creating a Quick Note or Temporary File:**`bash subl temp_note.md`
- **Opening a Specific Line in a File from a Build Error:**`bash # (Assume your build output says "Error: main.cpp:123") ERROR_MESSAGE="Error: main.cpp:123" FILENAME=$(echo "$ERROR_MESSAGE" | awk -F ':' '{print $1}') LINENO=$(echo "$ERROR_MESSAGE" | awk -F ':' '{print $2}') subl "$FILENAME":"$LINENO"`
