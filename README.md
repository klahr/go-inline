# go-script
This GitHub action allows you to use Go as a scripting language.

## Usage
### Basic

```yaml
steps:
  - uses: klahr/go-inline@v1
    with:
      source: |
        fmt.Println("Hello, world!")
```

### Set Go version
See https://github.com/actions/setup-go/tree/main/?tab=readme-ov-file#supported-version-syntax

```yaml
steps:
  - uses: klahr/go-inline@v1
    with:
      go-version: '1.20'
      source: |
        fmt.Println("Hello, world!")
```

### Custom template
The code specified in the source field is embedded into a minimal Go file. Refer to `action.yml` for the default value.
To have full control, you can override the default template by providing your own.

```yaml
steps:
  - uses: klahr/go-inline@v1
    with:
      template: |
        package main

        func main() {
            fmt.Println("My custom template")
            GO_SOURCE
        }
      source: |
        fmt.Println("Hello, world!")
```

### Dependencies
If you need to import external packages, you can use the `dependencies` field.

```yaml
steps:
    - uses: klahr/go-inline@v1
      with:
        dependencies: "github.com/google/uuid github.com/pkg/errors@v0.9.1"
        source: |
          id := uuid.New()
          fmt.Println(id.String())
          fmt.Println(errors.New("Hello, world!"))
```

### Step summary
The `GITHUB_STEP_SUMMARY` can be used to provide a summary of the step.

```yaml
steps:
    - uses: klahr/go-inline@v1
      with:
        source: |
        fmt.Println("Hello, world!")
        gha.WriteStepSummary("# A Header")
        gha.WriteStepSummary("## A Subheader")
```

### Set key/value
To pass values between steps, you can use the `gha.SetKeyValue` function.

```yaml
steps:
  - uses: klahr/go-inline@v1
    with:
      source: |
        gha.SetKeyValue("GITHUB_ENV", "MY_KEY", "my_value")

  - run: |
      echo "$MY_KEY"
```

## License
This project is licensed under the GPL v3.

## Contributions
We enthusiastically encourage and welcome contributions.
