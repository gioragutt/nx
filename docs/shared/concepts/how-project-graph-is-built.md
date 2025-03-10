# How the Project Graph is Built

Nx creates a graph of all the dependencies between projects in your workspace using two sources of information:

1. Package dependencies defined in the `package.json` file for each project.

   If the `myapp/package.json` file has this dependency:

   ```jsonc
   {
     "dependencies": {
       "@myorg/awesome-library": "*"
     }
   }
   ```

   Then `my-app` depends on `awesome-library`.

   Note: We typically use `*` for the dependency instead of a specific version because we want to depend on the version of the library as it currently exists in the repo.

2. Typescript `import` statements referencing a particular project's path alias

   For instance, if a file in `my-app` has this code:

   ```typescript
   import { something } from '@myorg/awesome-library';
   ```

   Then `my-app` depends on `awesome-library`

   This can be [turned on or off with the `analyzeSourceFiles` flag](../../recipe/analyze-source-files).

3. Manually created `implicitDependencies` in the project configuration file.

   If your project configuration has this content:

{% tabs %}
{% tab label="package.json" %}

```jsonc
{
  "name": "myapp",
  "nx": {
    "implicitDependencies": ["some-api"]
  }
}
```

{% /tab %}
{% tab label="project.json" %}

```jsonc
{
  "root": "/libs/myapp",
  "implicitDependencies": ["some-api"]
}
```

{% /tab %}
{% /tabs %}

Then `my-app` depends on `some-api`

## Related Documentation

### Recipes

- [Disable Graph Links Created from Analyzing Source Files](/recipe/analyze-source-files)
- [Modify the Project Graph with a Plugin](recipe/project-graph-plugins)
