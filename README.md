# elixir-vscode-docker-env

These files help create a docker development environment, in VS Code, for Elixir projects. This is currently setup for Elixir 1.11.0, Erlang OTP 23.1.1, and Ubuntu 18.04 LTS.

I basically copy these files and folders into a new Elixir or Phoenix project.

Remember to change the app name in the following files:

- .devcontainer/.devcontainer.json (line 2)
- docker-compose.yml (lines: 8, 22)
- .gitignore (line 26)

## Wallaby

Chromedriver will be installed in the docker container so that you can use Wallaby for testing as well. I currently use the following in my config/test.exs.

Example config/test.exs:

```Elixir
use Mix.Config

# Configure your database
#
# The MIX_TEST_PARTITION environment variable can be used
# to provide built-in test partitioning in CI environment.
# Run `mix help test` for more information.
config :appname_api, AppName.Repo,
  username: "postgres",
  password: "postgres",
  database: "appname_test#{System.get_env("MIX_TEST_PARTITION")}",
  hostname: "postgres",
  pool: Ecto.Adapters.SQL.Sandbox

# We don't run a server during test. If one is required,
# you can enable the server option below.
config :appname, AppNameWeb.Endpoint,
  http: [port: 4002],
  server: true

config :appname, :sql_sandbox, true

config :wallaby,
  driver: Wallaby.Experimental.Chrome,
  chrome: [headless: false]

# Print only warnings and errors during test
config :logger, level: :warn
```
