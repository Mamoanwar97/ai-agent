# LLM Agent

A powerful AI coding agent built with Google's Gemini API that can interact with your codebase through function calls. This agent can read files, execute Python scripts, write files, and perform various development tasks autonomously.

## Features

- 🤖 **AI-Powered Code Interaction**: Uses Google Gemini 2.0 Flash for intelligent code analysis and execution
- 🔧 **Function Calling**: Automatically calls appropriate functions based on user requests
- 📁 **File System Operations**: List, read, and write files with security constraints
- 🐍 **Python Execution**: Run Python scripts with arguments and capture output
- 🔍 **Verbose Mode**: Detailed logging for debugging and understanding agent behavior
- 🛡️ **Security**: Sandboxed execution within a working directory

## Available Functions

The agent has access to the following functions:

### `get_files_info`
Lists files and directories with metadata (size, type) within the working directory.

**Parameters:**
- `directory` (optional): Directory to list, relative to working directory

### `get_file_content`
Reads the contents of a file within the working directory.

**Parameters:**
- `file_path`: Path to the file to read, relative to working directory

### `write_file`
Creates or overwrites a file with specified content.

**Parameters:**
- `file_path`: Path to the file to write, relative to working directory
- `content`: Content to write to the file

### `run_python_file`
Executes a Python file with optional arguments and returns the output.

**Parameters:**
- `file_path`: Path to the Python file to execute
- `args` (optional): Array of arguments to pass to the script

## Installation

### Prerequisites
- Python 3.10 or higher
- UV package manager (recommended) or pip

### Setup

1. **Clone the repository:**
   ```bash
   git clone <repository-url>
   cd llm-agent
   ```

2. **Install dependencies:**
   ```bash
   # Using UV (recommended)
   uv sync
   
   # Or using pip
   pip install -r requirements.txt
   ```

3. **Set up environment variables:**
   Create a `.env` file in the project root:
   ```bash
   GEMINI_API_KEY=your_gemini_api_key_here
   ```

4. **Get a Gemini API key:**
   - Visit [Google AI Studio](https://aistudio.google.com/)
   - Create a new API key
   - Add it to your `.env` file

## Usage

### Basic Usage

```bash
python main.py "Your request here"
```

### Examples

**List files in a directory:**
```bash
python main.py "List all files in the calculator directory"
```

**Read a file:**
```bash
python main.py "Read the contents of calculator/main.py"
```

**Execute a Python script:**
```bash
python main.py "Run the calculator with the expression '3 + 5'"
```

**Write a new file:**
```bash
python main.py "Create a new file called test.py with a simple hello world program"
```

### Verbose Mode

Add the `--verbose` or `-v` flag for detailed output:

```bash
python main.py --verbose "Your request here"
```

Verbose mode shows:
- Function calls being made
- API key preview (first 10 characters)
- Detailed token usage
- Step-by-step execution

## Project Structure

```
llm-agent/
├── main.py                 # Main application entry point
├── functions/             # Function implementations
│   ├── get_files_info.py  # File listing functionality
│   ├── get_file_content.py # File reading functionality
│   ├── write_file.py     # File writing functionality
│   ├── run_python_file.py # Python execution functionality
│   └── verbose_function.py # Function call orchestration
├── calculator/            # Example calculator application
│   ├── main.py           # Calculator entry point
│   ├── tests.py          # Calculator tests
│   └── pkg/              # Calculator package
├── .env                  # Environment variables (create this)
├── pyproject.toml        # Project dependencies
└── README.md            # This file
```

## Configuration

### Working Directory
The agent operates within a sandboxed working directory (default: `./calculator`). All file operations are restricted to this directory for security.

### Security Features
- **Path Validation**: All file operations are validated to ensure they stay within the working directory
- **Sandboxed Execution**: Python scripts run in a controlled environment
- **Timeout Protection**: Script execution is limited to 30 seconds
- **Error Handling**: Comprehensive error handling for all operations

## Development

### Running Tests
```bash
python tests.py
```

### Adding New Functions
1. Create a new function in the `functions/` directory
2. Add the function schema to the available functions list in `main.py`
3. Update the `verbose_function.py` to handle the new function

### Example Function Structure
```python
def my_function(working_directory, param1, param2=None):
    # Function implementation
    return result

schema_my_function = types.FunctionDeclaration(
    name="my_function",
    description="Description of what the function does",
    parameters=types.Schema(
        type=types.Type.OBJECT,
        properties={
            "param1": types.Schema(
                type=types.Type.STRING,
                description="Description of param1"
            ),
            "param2": types.Schema(
                type=types.Type.STRING,
                description="Description of param2"
            )
        },
        required=["param1"]
    )
)
```

## Troubleshooting

### Common Issues

**"GEMINI_API_KEY environment variable not set"**
- Ensure you have created a `.env` file with your API key
- Check that the `.env` file is in the project root directory

**"Error: Cannot access file outside working directory"**
- The agent is restricted to the working directory for security
- Use relative paths within the working directory

**"Error executing Python file"**
- Ensure the file exists and is a valid Python file
- Check that the file path is relative to the working directory

### Debug Mode
Use verbose mode to see detailed execution information:
```bash
python main.py --verbose "Your request"
```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is open source. Please check the license file for details.

## Support

For issues and questions:
1. Check the troubleshooting section above
2. Review the verbose output for error details
3. Open an issue on the repository

---

**Note**: This agent is designed for development and automation tasks. Always review the agent's actions, especially when writing or modifying files.
