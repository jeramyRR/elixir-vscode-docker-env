# elixir-vscode-docker-env

These files help create a docker development environment for Elixir projects. This is currently setup for Elixir 1.11.0, Erlang OTP 23.1.1, and Ubuntu 18.04 LTS.

I basically copy these files and folders into a new Elixir or Phoenix project.

Remember to change the app name in the following files:

- .devcontainer/.devcontainer.json (line 2)
- docker-compose.yml (lines: 8, 22)
- .gitignore (line 26)
