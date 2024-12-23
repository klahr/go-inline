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

## License
This project is licensed under the GPL v3.

## Contributions