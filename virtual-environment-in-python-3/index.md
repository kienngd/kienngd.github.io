# Virtual environment in Python 3


## What is a virtual environment?

A virtual environment is a separate Python environment. It is isolated from your system's Python environment. It lets you install Python packages and libraries. These packages don't affect other projects or your system's Python.

<!--more-->

## Why use a virtual environment?

* **Isolate projects:** Each project may need different packages and versions. A virtual environment helps you manage these dependencies. It keeps projects separate and avoids conflicts.
* **Easy dependency management:** You can easily install, upgrade, or remove packages in a virtual environment. This doesn't affect other projects.
* **Keep your system clean:** A virtual environment keeps your system's Python clean. It avoids conflicts and makes things easier to manage.

## `venv` - Built-in tool in Python

`venv` is a module in Python 3. It's easy to use for creating and managing virtual environments.

## Example of using `venv`

1. **Create a virtual environment:**

   ```bash
   python3 -m venv myenv
   ```

   This makes a new virtual environment named `myenv`. It's in the current folder.

2. **Activate the virtual environment:**

   * **Linux/macOS:**
     ```bash
     source myenv/bin/activate
     ```

   * **Windows:**
     ```bash
     myenv\Scripts\activate
     ```

   You'll see the virtual environment's name in the command prompt. This means it's active.

3. **Choose an interpreter:**

    If you use **VSCode** for Python development and want it to use the interpreter from your virtual environment, instead of the default Python installed on your machine, you can do the following:

    * Press `Ctrl + Shift + P` to open the command palette.
    * Type `Python: Select Interpreter` and press Enter.
    * Choose the correct interpreter from your virtual environment.

    This will tell VSCode to use the Python interpreter inside your virtual environment for your project.


4. **Deactivate the virtual environment:**

   ```bash
   deactivate
   ```

5. **Delete the virtual environment:**

   Just delete the virtual environment's folder.

## Other tools

Besides `venv`, there are other tools for managing virtual environments. For example:

* `virtualenv`
* `conda`

## Conclusion

A virtual environment is a useful tool. It helps you manage Python projects well. I hope this article helps you understand virtual environments and how to use them.
