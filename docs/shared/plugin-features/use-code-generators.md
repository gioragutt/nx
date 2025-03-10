# Use Code Generators

Generators provide a way to automate many tasks you regularly perform as part of your development workflow. Whether it is scaffolding out components, features, ensuring libraries are generated and structured in a certain way, or updating your configuration files, generators help you standardize these tasks in a consistent, and predictable manner.

## Types of Generators

There are three main types of generators:

1. **Plugin Generators** are available when an Nx plugin has been installed in your workspace.
2. **Workspace Generators** are generators that you can create for your own workspace. [Workspace generators](/recipe/workspace-generators) allow you to codify the processes that are unique to your own organization.
3. **Update Generators** are invoked by Nx plugins when you [update Nx](/recipes/adopting-nx) to keep your config files in sync with the latest versions of third party tools.

## Invoking Plugin Generators

Generators allow you to create or modify your codebase in a simple and repeatable way. Generators are invoked using the [`nx generate`](/nx/generate) command.

```bash
nx generate [plugin]:[generator-name] [options]
nx generate @nrwl/react:component mycmp --project=myapp
```

It is important to have a clean git working directory before invoking a generator so that you can easily revert changes and re-invoke the generator with different inputs.

## Related Documentation

### Concepts

- [Using Nx at Enterprises](/more-concepts/monorepo-nx-enterprise)

### Recipes

- [Workspace Generators](/recipe/workspace-generators)
- [Composing Generators](/recipe/composing-generators)
- [Generator Options](/recipe/generator-options)
- [Creating Files](/recipe/creating-files)
- [Modifying Files](/recipe/modifying-files)

### Reference

- [generate command](/nx/generate)
- [nx.json defaultCollection property](/reference/nx-json#cli-options)
- [nx.json generator defaults](/reference/nx-json#generators)
