# elixir-tips-tricks
Just random tips and tricks while working with elixir [&amp; phoenix and other libs/frameworks]


### Disable compiling of dependency in mix
```
{:my_dep, …, compile: false}
```

### Run only particular tests

Use `@tag :wip` in the test you want to run
```
defmodule MyTest do
  use ExUnit.Case
  
  test "first test" do
    assert 1 == 1
  end
  
  @tag :wip
  test "second test" do
    assert 3 != 5
  end
end
```

```
mix test --only wip
```

### Build composable queries with Inquisitor
Check the [Inquisitor](https://github.com/DockYard/inquisitor) repository if you're looking for building composable queries for Ecto.

### iex shortcuts
- c "somefile.exs" - compile the file
- r SomeModule - reload the module
- h some_func - get help for the function
- v [n] - access session history

### Get query and post params excluding others in params (phoenix)

```
conn.body_params # gives params from POST
conn.query_params # query string parameters
```

### Run multiple mix tasks

```
MIX_ENV=test mix do deps.get, test
```

### Update particular dependency

```
mix deps.update <dep_name>
```

### Turn off layout on Phoenix.Controller.render/3

```
render conn, "index.html", %{layout: false}
# with plug
plug :put_layout, false

# pipe it
conn |> put_layout(false) |> render(...)
```

### Increase stacktrace

```
:erlang.system_flag(:backtrace_depth, 20)

# with phoenix
# config/env.exs
config :phoenix, :stacktrace_depth, 20
```

### Observer on remote erlang node

```
$ iex --name phoenix@127.0.0.1 --cookie iam_not_so_awesome -S mix phoenix.server  # in api server

# on separate shell
$ iex --name test@127.0.0.1 --remsh phoenix@127.0.0.1 --cookie iam_not_so_awesome
iex(phoenix@127.0.0.1)1> :observer.start
```

You can pass args down to erlang via `erl` flag.
Example: `--erl "-kernel inet_dist_listen_min 9001 inet_dist_listen_m 9001"`

### Change default compile output directory

Based on [this](https://github.com/elixir-lang/elixir/blob/4e648199f18ee3be8addab82c951b9e2dd82f885/lib/mix/lib/mix/tasks/new.ex#L286), you can specify a keyword list arg `build_path` to override the default `_build` directory.

Example:

    def project do
        [app: :my_app,
        version: "0.0.1",
        elixir: "~> 1.2",
        build_embedded: Mix.env == :prod,
        start_permanent: Mix.env == :prod,
        build_path: "custom_build_dir",
        deps: deps]
    end

### Emmet tab support for eex in Atom

Open your preferences and select keymaps. It should open keymaps.cson. Add the following in that file:

```coffeescript
'atom-text-editor[data-grammar="text html elixir"]:not([mini])':
    'tab': 'emmet:expand-abbreviation-with-tab'
```
