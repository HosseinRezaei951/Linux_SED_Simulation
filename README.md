# Linux SED Simulation - CSED

## Project Overview

The **Linux SED Simulation** project involves creating a Python-based utility called `csed`, designed to emulate the basic functionalities of the `sed` command in Linux. This utility supports various stream editing tasks such as printing specific lines from a file, replacing text within files or pipeline inputs, and handling both simple and complex text substitutions. The `csed` script is designed to be run directly from the terminal, similar to the native `sed` command, and can process both files and input streams.

## Features and Functionalities

### 1. Print Input Stream with `-n` Parameter

This feature allows the user to print a specified range of lines from the input stream or a file. The `-n` option suppresses automatic printing and only prints the lines specified by the script.

- **Usage**:
  ```bash
  csed -n 'startLineNumber,endLineNumberp' [INPUTFILE]
  ```

- **Script Syntax**:
  - The script `startLineNumber,endLineNumberp` specifies the range of lines to print.
  - If `startLineNumber` is omitted, it defaults to 1 (the first line).
  - If `endLineNumber` is omitted, it defaults to the last line in the input stream or file.

- **Example**:
  ```bash
  csed -n '5,10p' input.txt
  # Prints lines 5 to 10 from input.txt
  ```

### 2. Simple Replacing without Parameters

This feature allows the user to replace the first occurrence of a specified string (`oldString`) with a new string (`newString`) in each line of the input stream or file. The result is printed to the standard output.

- **Usage**:
  ```bash
  csed 's/oldString/newString/' [INPUTFILE]
  ```

- **Script Syntax**:
  - `s/oldString/newString/` replaces the first occurrence of `oldString` with `newString` in each line.

- **Example**:
  ```bash
  csed 's/hello/hi/' input.txt
  # Replaces the first occurrence of "hello" with "hi" in each line of input.txt
  ```

### 3. Complex Replacing without Parameters

This feature extends the simple replace functionality by allowing for global replacements or line-specific replacements.

- **Usage**:
  ```bash
  csed 's/oldString/newString/[g/lineNumber]' [INPUTFILE]
  ```

- **Script Syntax**:
  - `s/oldString/newString/g` replaces all occurrences of `oldString` with `newString` in each line.
  - `s/oldString/newString/lineNumber` replaces `oldString` with `newString` only on the specified line number.

- **Example**:
  ```bash
  csed 's/foo/bar/g' input.txt
  # Replaces all occurrences of "foo" with "bar" in each line of input.txt
  ```

### 4. Complex Replacing with `-i` Parameter

This feature performs the same complex replacement as described above but with the addition of the `-i` option, which allows the changes to be saved directly back to the input file rather than just printing the results.

- **Usage**:
  ```bash
  csed -i 's/oldString/newString/[g/lineNumber]' [INPUTFILE]
  ```

- **Script Syntax**:
  - Same as the complex replacing without parameters, but the `-i` option ensures that the changes are saved to the file.

- **Example**:
  ```bash
  csed -i 's/foo/bar/g' input.txt
  # Replaces all occurrences of "foo" with "bar" in each line of input.txt and saves the changes in the file
  ```

## Implementation Details

### File Class (`FILE`)

- **Purpose**: Handles the reading, writing, and manipulation of file contents or pipeline input.
- **Key Methods**:
  - `read_file(path)`: Reads the contents of a file into the object.
  - `get_pipeInput(pipeInput)`: Reads the contents of pipeline input into the object.
  - `print_lines(start, end)`: Prints specified lines from the file or pipeline input.
  - `save_file()`: Saves the modified content back to the original file.

### CSED Class (`CSED`)

- **Purpose**: Implements the core functionality of the `csed` command, including parsing options and scripts, and executing the appropriate actions.
- **Key Methods**:
  - `check_INPUTFILE()`: Validates the input file or pipeline.
  - `check_OPTIONS()`: Determines the action based on the options and script provided.
  - `printInputStream()`: Handles printing a specified range of lines.
  - `replacing()`: Performs string replacement operations based on the script provided.

### Error Handling

- The script is designed to be robust with comprehensive error handling. If any invalid input or script is detected, the script will terminate with an appropriate error message.

## Installation and Usage

1. **Convert the Script to an Executable**:
   Ensure the script is executable and can be run directly from the terminal.
   ```bash
   chmod +x csed
   ```

2. **Add to System PATH**:
   To make the `csed` command available globally, move it to a directory included in the system's PATH.
   ```bash
   sudo cp csed /usr/local/bin/
   ```

3. **Run the Script**:
   The script can now be executed from any directory in the terminal as if it were a native command.

## Conclusion

The `csed` utility is a simplified emulation of the Linux `sed` command, designed for stream editing tasks such as printing specific lines and replacing text in files or input streams. It supports both simple and complex replacements, with the ability to modify files in place using the `-i` option.
