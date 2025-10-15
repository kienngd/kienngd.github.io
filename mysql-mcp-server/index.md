# Getting Started with MySQL MCP Server


## Getting Started with MySQL MCP Server Locally

This guide shows you how to set up and use the MySQL Model Context Protocol (MCP) Server on your local machine, focusing on integration with Cursor, an AI-powered code editor.

## What is MySQL MCP Server?

MySQL MCP Server is a tool that lets AI applications, like Cursor, safely interact with your MySQL database. Instead of writing raw SQL, you can ask questions about your data. The server handles the communication, making database access more structured and secure.

[Main github repository is here](https://github.com/designcomputer/mysql_mcp_server)
<!--more-->
## Installing and Configuring with Cursor

First, make sure your system has Python and `uv` installed. `uv` is a fast Python package installer and resolver.

1.  **Install the Server:** Open your terminal and run the installation command for Cursor:
    ```bash
    npx -y @smithery/cli install mysql-mcp-server --client cursor
    ```
    This command automatically configures the server to work with Cursor.

2.  **Set Up Environment Variables:** The server needs to know how to connect to your MySQL database. Create or edit a file called `cursor_mcp_config.json` in your Cursor settings directory (usually `~/.cursor/mcp/` on macOS/Linux or `%APPDATA%\cursor\mcp\` on Windows). Add the following content, replacing the placeholder values with your actual database credentials:

    ```json
    {
      "servers": {
        "mysql": {
          "type": "stdio",
          "command": "uvx",
          "args": [
            "--from",
            "mysql-mcp-server",
            "mysql_mcp_server"
          ],
          "env": {
            "MYSQL_HOST": "localhost",
            "MYSQL_PORT": "3306", // Default MySQL port
            "MYSQL_USER": "your_username",
            "MYSQL_PASSWORD": "your_password",
            "MYSQL_DATABASE": "your_database_name"
          }
        }
      }
    }
    ```

    **Security Note:** Never share these credentials or commit them to code repositories. Use a dedicated MySQL user with minimal necessary permissions.

3.  **Restart Cursor:** Close and reopen Cursor to apply the new configuration.

## Using the MySQL Tool in Cursor

Once configured and Cursor is restarted, the MySQL MCP Server is active.

*   **Ask Questions:** You can now ask Cursor questions about your database schema or data within your editor. For example, you might type a prompt like "Show me the structure of the 'users' table" or "How many records are in the 'orders' table?". Cursor will use the MCP server to fetch this information.
*   **List Tables:** The server allows Cursor to list available tables in your configured database, helping you understand the data structure.

## Developing the Tool Locally

If you want to modify the MySQL MCP Server itself, you can download the source code and run it locally during development.

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/designcomputer/mysql_mcp_server.git
    cd mysql_mcp_server
    ```

2.  **Set Up a Virtual Environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate # On Windows: venv\Scripts\activate
    ```

3.  **Install Development Dependencies:**
    ```bash
    pip install -r requirements-dev.txt
    ```

4.  **Run Tests (Optional but Recommended):**
    ```bash
    pytest
    ```

You can now edit the Python files in the repository. Remember to set the required environment variables (like `MYSQL_HOST`, `MYSQL_USER`, etc.) in your shell or a `.env` file before running any local scripts for testing.

The server is designed to work with AI applications via the MCP standard and is not meant to run as a standalone program. Use tools like the MCP Inspector for deeper debugging if needed.
