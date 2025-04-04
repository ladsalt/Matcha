# Matcha

Matcha is a Python-based tool designed to streamline the management of Python projects with virtual environments and dependencies. It simplifies the process of creating virtual environments, installing dependencies, and running your projects based on configurations stored in simple JSON files.

## Features

* **Virtual Environment Management:** Easily create and manage multiple virtual environments for your project.
* **Dependency Management:** Define project dependencies and their versions in a JSON configuration file. Matcha will handle the installation.
* **Configuration Separation:** Project-specific settings are stored in a `matcha` file, while Matcha's settings are stored in `matcha-config`.
* **Flexible Project Directory:** Run projects from any directory using the `--dir` option.
* **Message Filtering:** Control the output of error, warning, and info messages.
* **Simple JSON Configuration:** Use easy-to-understand JSON files to configure your projects.

## Setup

1.  **Project Directory:**
    * Create a directory for your project.
    * Inside this directory, create the `matcha` file for project-specific configurations.

2.  **`matcha` File:**
    * Create a file named `matcha` (without any file extension).
    * This file will contain your project's configuration in JSON format.
    * Example `matcha` file:

        ```json
        {
          "project-info": {
            "project-name": "MyProject",
            "project-source": "src/main.py",
            "version": "1.0.0"
          },
          "venv-configs": {
            "main-venv": {
              "main": true
            },
            "dev-venv": {}
          },
          "dependencies": {
            "requests": {
              "venv": "main-venv",
              "version": "2.26.0"
            },
            "numpy": {
              "venv": "dev-venv",
              "version": "1.21.0"
            },
            "flask": {
              "venv": "main-venv"
            }
          }
        }
        ```

    * **Explanation:**
        * `project-info`: Defines the project's name, main script, and version.
        * `venv-configs`: Specifies the virtual environments to create. The `main: true` field denotes the main virtual environment.
        * `dependencies`: Lists the Python packages to install and the virtual environment they should be installed in. If a version is provided, that specific version will be installed; otherwise, the latest version will be used.

3.  **`matcha-config` File (Optional):**
    * Create a file named `matcha-config` (without any file extension) in the same directory as the `matcha.py` script.
    * This file will contain Matcha's settings.
    * Example `matcha-config` file:

        ```json
        {
          "ignore": {
            "errors": false,
            "warnings": false,
            "info": false
          }
        }
        ```

    * **Explanation:**
        * `ignore`: Controls the display of error, warning, and info messages. Setting a value to `true` will suppress that type of message.

4.  **Running Matcha:**
    * Open your terminal or command prompt.
    * Navigate to the directory containing `matcha.py`.
    * Use the `--dir` option to specify the directory containing your `matcha` file.

## Usage

### Commands

* **`info`:** Displays project information.

    ```bash
    python matcha.py info --dir=/path/to/my/project
    ```

    * This command will output the project's name, source, version, and main virtual environment.

* **`run`:** Creates virtual environments, installs dependencies, and runs the project.

    ```bash
    python matcha.py run --dir=/path/to/my/project
    ```

    * This command will:
        * Create the virtual environments specified in the `matcha` file.
        * Install the dependencies in their respective virtual environments.
        * Activate the main virtual environment.
        * Run the project's main script (specified in `project-source`).

### Examples

1.  **Running the project with message filtering:**

    * `matcha-config`:

        ```json
        {
          "ignore": {
            "info": true
          }
        }
        ```

    * Command:

        ```bash
        python matcha.py run --dir=/path/to/my/project
        ```

    * In this case, any info messages generated by Matcha will be suppressed.

2.  **Running the project from a different directory:**

    * Assuming your `matcha` file is located at `/home/user/my-projects/my-app/matcha`.
    * Command:

        ```bash
        python /path/to/matcha.py run --dir=/home/user/my-projects/my-app
        ```

    * Matcha will use the `matcha` file located at the specified directory.

## Contributing

Contributions are welcome! Please feel free to submit pull requests or open issues for bug reports or feature requests.
