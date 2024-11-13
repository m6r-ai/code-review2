# code-review2

A command-line tool for AI-assisted code reviews that leverages the Metaphor language format to generate structured review prompts.

## Overview

code-review2 is a Python-based command-line application that helps developers get AI-powered code reviews. It takes your source code files and review guidelines as input, then generates a properly formatted prompt that can be used with AI systems to perform detailed code reviews.

## Features

- Process multiple source files for review
- Support for custom review guidelines using Metaphor (.m6r) files
- Flexible search paths for finding guideline files
- Output to file or stdout
- Comprehensive error handling and reporting

## Installation

The application requires Python 3 and the m6rclib package. Ensure both are installed before using the tool.

## Usage

Basic syntax:
```bash
code-review2.py [options] file1 [file2 ...]
```

### Command Line Options

- `-h, --help`: Show help message and exit
- `-v, --version`: Show program's version number and exit
- `-o OUTPUT, --output OUTPUT`: Specify output file (defaults to stdout)
- `-g PATH, --guideline-path PATH`: Add a directory to search for .m6r files (defaults to current directory)

### Examples

Review a single file using guidelines in the current directory:
```bash
code-review2.py src/myfile.py
```

Review multiple files and save the prompt to a file:
```bash
code-review2.py -o review-prompt.txt src/file1.py src/file2.py
```

Use guidelines from multiple directories:
```bash
code-review2.py -g ./guidelines -g ./custom-guidelines src/myfile.py
```

## Review Guidelines

The tool searches for Metaphor guideline files (*.m6r) in:
1. The current working directory (default)
2. Any directories specified with the `-g` option

At least one valid guideline file must be found for the tool to work.

The tool will include all guidelines it can find.  If you want to add new ones for a particular language then
create a new file for that language and add content in the same format as the examples provides.

## Exit Codes

The application uses the following exit codes:
- 0: Success
- 1: Command line usage error
- 2: Data format error (e.g., invalid Metaphor syntax)
- 3: Cannot open input file
- 4: Cannot create output file

## Error Handling

The tool provides detailed error messages when issues occur:
- Missing input files
- Invalid command line arguments
- Missing guideline files
- Syntax errors in Metaphor files
- File access problems

Error messages are written to stderr and include:
- Clear description of the error
- Filename (when relevant)
- Line number and column (for syntax errors)

## Output Format

The tool generates a structured prompt using the Metaphor language format, which includes:
1. A role definition for the AI reviewer
2. Review guidelines from .m6r files
3. The files to be reviewed
4. Specific instructions for the review process

The output can be directed to:
- stdout (default)
- A file specified with the `-o` option

## Limitations

- The tool requires at least one .m6r guideline file to be present
- Input files must be text-based source code files
- Large files may need to be reviewed in segments

## Troubleshooting

Common issues and solutions:

1. "No .m6r guideline files found":
   - Check that guideline files exist in the search paths
   - Verify file extensions are correctly set to .m6r
   - Use -g to specify additional search paths

2. "Cannot open input file":
   - Verify the file exists
   - Check file permissions
   - Ensure the path is correct

3. "Cannot create output file":
   - Check write permissions in the target directory
   - Verify the path is valid
   - Ensure sufficient disk space

## Support

For more information or to report issues, please refer to the project's documentation or issue tracker.