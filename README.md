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

### Get query and post params excluding others in params

```
conn.body_params # gives params from POST
conn.query_params # query string parameters
```
