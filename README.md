# tya-cli

A small dry-cli style command framework for Tya.

```tya
import cli/*

class HelloCommand extends cli.Command
  name: "hello"
  description: "Print a greeting"
  arguments: [cli.Spec.argument("name", "Name to greet")]

  call: invocation ->
    name = invocation.params["name"]
    if name == nil
      name = "world"
    cli.Result.success("Hello, {name}!")

class ExampleApp extends cli.Application
  name: "example"
  commands: [HelloCommand()]

app = ExampleApp()
app.run(["hello", "Tya"])
```

Root commands can also define their own arguments and options.

```tya
class ConvertApp extends cli.Application
  name: "convert"
  description: "Convert files"
  arguments: [
    cli.Spec.argument("input", "Input file", { required: true }),
    cli.Spec.argument("output", "Output file", { required: true })
  ]
  options: [
    cli.Spec.option("format", "Output format", { default: "png" }),
    cli.Spec.boolean_option("overwrite", "Overwrite output file", false, { aliases: ["-f"] })
  ]

  call: invocation ->
    input = invocation.params["input"]
    output = invocation.params["output"]
    cli.Result.success("{input} -> {output}")
```
