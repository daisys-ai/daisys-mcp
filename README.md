# Daisys MCP server
[![smithery badge](https://smithery.ai/badge/@daisys-ai/daisys-mcp)](https://smithery.ai/server/@daisys-ai/daisys-mcp)

Daisys-mcp is a beta version and doesn't have a stable release yet. But you can try it out by doing the following:

1. Get an account on [Daisys](https://www.daisys.ai/) and create an username and password.


If you run on mac os run the following command:
```bash
brew install portaudio
```

If you run on linux run the following command:
```bash
sudo apt install portaudio19-dev libjack-dev
```

2. Add the following configuration to the mcp config file in your MCP client ([Claude Desktop](https://claude.ai/download), [Cursor](https://www.cursor.com/), [mcp-cli](https://github.com/chrishayuk/mcp-cli), [mcp-vscode](https://code.visualstudio.com/docs/copilot/chat/mcp-servers), etc.):
```json
{
  "mcpServers": {
    "daisys-mcp": {
      "command": "uvx",
      "args": ["daisys-mcp"],
      "env": {
        "DAISYS_EMAIL": "{Your Daisys Email}",
        "DAISYS_PASSWORD": "{Your Daisys Password}",
        "DAISYS_BASE_STORAGE_PATH": "{Path where you want to store your audio files}"
      }
    }
  }
}
```

## To build from source:

1. clone the repository: `git clone https://github.com/daisys-ai/daisys-mcp.git`

2. cd into the repository: `cd daisys-mcp`

3. Install `uv` (Python package manager), install with `curl -LsSf https://astral.sh/uv/install.sh | sh` or see the `uv` [repo](https://github.com/astral-sh/uv) for additional install methods.

4. Create a virtual environment and install dependencies [using uv](https://github.com/astral-sh/uv):

```bash
uv venv
# source .venv/Scripts/activate (Windows)
source .venv/bin/activate (mac and linux)
uv pip install -e .
```

5. Add the following to your config file in your MCP client ([Claude Desktop](https://claude.ai/download), [Cursor](https://www.cursor.com/), [mcp-cli](https://github.com/chrishayuk/mcp-cli), [mcp-vscode](https://code.visualstudio.com/docs/copilot/chat/mcp-servers), etc.):
```json
{
    "mcpServers": {
        "daisys-mcp": {
            "command": "uv",
            "args": [
                "--directory",
                "{installation_path}/daisys-mcp",
                "run",
                "-m",
                "daisys_mcp.server"
            ],
            "env": {
                "DAISYS_EMAIL": "{Your Daisys Email}",
                "DAISYS_PASSWORD": "{Your Daisys Password}",
                "DAISYS_BASE_STORAGE_PATH": "{Path where you want to store your audio files}"
            }
        }
    }
}
```

## Common Issues

If you get any issues with portaudio on linux, you can try installing it manually:
```bash
sudo apt-get update
sudo apt-get install -y portaudio19-dev
```

## Contributing

If you want to contribute or run from source:

1. Clone the repository:

```bash
git clone https://github.com/daisys-ai/daisys-mcp.git
cd daisys_mcp
```

2. Create a virtual environment and install dependencies [using uv](https://github.com/astral-sh/uv):

```bash
uv venv
source .venv/bin/activate
uv pip install -e .
uv pip install -e ".[dev]"
```

3. Copy `.env.example` to `.env` and add your DAISYS username and password:

```bash
cp .env.example .env
# Edit .env and add your DAISYS username and password
```

4. Test the server by running the tests:

```bash
uv run pytest
```

you can also run a full integration test with:

```bash
uv run pytest -m 'requires_credentials' # ⚠️ Running full integration tests does costs tokens on the Daisys platform 
```

5. Debug and test locally with MCP Inspector: `uv run mcp dev daisys_mcp/server.py`
