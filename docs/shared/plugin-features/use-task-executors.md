# Use Task Executors

Executors perform actions on your code. This can include building, linting, testing, serving and many other actions.

There are two main differences between an executor and a shell script or an npm script:

1. Executors encourage a consistent methodology for performing similar actions on unrelated projects. i.e. A developer switching between teams can be confident that `nx build project2` will build `project2` with the default settings, just like `nx build project1` built `project1`.
2. Nx can leverage this consistency to run the same target across multiple projects. i.e. `nx affected --target=test` will run the `test` executor associated with the `test` target on every project that is affected by the current code change.
3. Executors provide metadata to define the available options. This metadata allows the Nx CLI to show prompts in the terminal and Nx Console to generate a GUI for the executor.

## Executor definitions

Executors are associated with specific targets in a project's `project.json` file.

```json
{
  "root": "apps/cart",
  "sourceRoot": "apps/cart/src",
  "projectType": "application",
  "generators": {},
  "targets": {
    "build": {
      "executor": "@nrwl/web:webpack",
      "options": {
        "outputPath": "dist/apps/cart",
        ...
      },
      "configurations": {
        "production": {
          "sourceMap": false,
          ...
        }
      }
    },
    "test": {
      "executor": "@nrwl/jest:jest",
      "options": {
        ...
      }
    }
  }
}
```

Each project has targets configured to run an executor with a specific set of options. In this snippet, `cart` has two targets defined - `build` and `test`.

{% callout type="note" title="More details" %}
`build` and `test` can be any strings you choose. For the sake of consistency, we make `test` run unit tests for every project and `build` produce compiled code for the projects which can be built.
{% /callout %}

Each executor definition has an `executor` property and, optionally, an `options` and a `configurations` property.

- `executor` is a string of the form `[package name]:[executor name]`. For the `build` executor, the package name is `@nrwl/web` and the executor name is `webpack`.
- `options` is an object that contains any configuration defaults for the executor. These options vary from executor to executor.
- `configurations` allows you to create presets of options for different scenarios. All the configurations start with the properties defined in `options` as a baseline and then overwrite those options. In the example, there is a `production` configuration that overrides the default options to set `sourceMap` to `false`.

## Running executors

The [`nx run`](/nx/run) cli command (or the shorthand versions) can be used to run executors.

```bash
nx run [project]:[command]
nx run cart:build
```

As long as your command name doesn't conflict with an existing nx cli command, you can use this short hand:

```bash
nx [command] [project]
nx build cart
```

You can also use a specific configuration preset like this:

```bash
nx [command] [project] --configuration=[configuration]
nx build cart --configuration=production
```

Or you can overwrite individual executor options like this:

```bash
nx [command] [project] --[optionNameInCamelCase]=[value]
nx build cart --outputPath=some/other/path
```

## Related Documentation

### Concepts

- [Task Pipeline Configuration](/concepts/task-pipeline-configuration)
- [Incremental Builds](/more-concepts/incremental-builds)

### Recipes

- [Use Executor Configurations](/recipe/use-executor-configurations)
- [Running Custom Commands](/recipe/run-commands-executor)
- [Creating Custom Executors](/recipe/creating-custom-executors)
- [Compose Executors](/recipe/compose-executors)
- [Faster Builds with Module Federation](/recipe/faster-builds)
- [Customizing Webpack Config](/recipe/customize-webpack)
- [Profiling Performance](/recipe/performance-profiling)

### Reference

- [run command](/nx/run)
- [run-many command](/nx/run-many)
- [affected command](/nx/affected)
- [Project Configuration](/reference/project-configuration)
