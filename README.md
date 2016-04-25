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
