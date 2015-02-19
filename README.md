# rOpenSci Style Guide

The following are in-development style guidelines for contributed packages to rOpenSci. Use [issues](https://github.com/ropensci/styleguide/issues) to discuss these.

This guide includes a bit more than what would typically be in a style guide. We are developing a separate set of policies which we'll enforce, while this guide includes suggestions for developing packages contributed to rOpenSci. Thus, this guide needs to include more than just style.

## Package naming

Although we have been inconsistent in the past, we'd like to make package naming consistent moving forward. Consider the following: 

* Use all lowercase letters, unless `camelCase`, etc. makes more sense, e.g., the `XML` package makes sense to have uppercase letters since the XML is most often referred to in uppercase
* Make sure that the package name isn't already taken 
    * Look at the [list of available packages](http://cran.rstudio.com/web/packages/available_packages_by_name.html)
    * When you run check on your package, the process will ping CRAN to make sure there isn't a package name conflict
* The GitHub repository name should match the package name. Note that valid package names cannot have hyphens. This makes everything much easier in the long run. In addition, avoid having the package as a sub-directory within the root of the repository.
* Make sure that the name you choose does not make the entity that provides the data upset - e.g., they may not want you to use their name as part of the package name (e.g., Acme may not want you to name R package `acme`)

## Function/variable naming

We prefer `snake_case` over all other styles, though if you're bringing over a package that's been around for a while with something else, e.g., `camelCase`, that's fine. Do not in most cases use function or variable names that already exist in base R or other packages. Of course, you aren't expected to go check all other packages, though you can do a quick check at, for example, [R-Documentation.org](http://www.rdocumentation.org/).

## Syntax

Follow [Hadley's guidelines on syntax](http://adv-r.had.co.nz/Style.html). In short: 

* Spacing: use appropriate spacing around infix operators (`x = 5` instead of `x=5`)
* Curly braces: open curly brace never goes on its own line, closing curly brace goes on its own line unless followed by `else`
* Line length: Limit each line to 80 characters. This is easier to read, and `R CMD CHECK` does check this (though checks for `< 100`)
* Assignment: Use `<-`, not `=`

## Files and file names

Use meaningful names like `optim.R` instead of `aaaa.r` if the function within is named `optim()`. In addition, try to avoid piling many unrelated functions in a single file, so that the file `optim.R` really only has the function `optim()` and any helper functions only used by it. Internal helper functions used across many functions should go in a separate file, e.g. `utils.R`. Naming files so that others can easily find things makes collaborative development easier

## Documentation

We strongly encourage all submissions to use `roxygen2` for documentation.  `roxygen2` is [an R package](http://cran.r-project.org/web/packages/roxygen2/index.html) that automatically compiles your `.Rd` files to your `man` folder in your package if you write the documentation following a few rules.

Check out [Hadley's devtools wiki](https://github.com/hadley/devtools/wiki/Documenting-functions) for advice on using `roxygen2` to document R functions.

By using `roxygen2`, this means you can generate your `NAMESPACE` automatically - please avoid simply exporting all your internal functions.

## Examples

Include extensive examples in the documentation. In addition to demonstrating how to use the package, these can act as an easy way to test package functionality before there are proper tests. However, keep in mind we require tests in contributed packages. If you prefer not to clutter up code with extensive documentation, place further documentation/examples in files in a `man-roxygen` folder in the root of your package, and those will be combined into the manual file by the use of `@template <file name>`, for example.

## Package dependencies

Use `Imports` instead of `Depends` for packages providing functions you use internally only. Use `Depends` only if you intend for the user to have functions available from your package dependencies.

## Expose options to the user

When calling another function internally, such as `optim()`, pass all the function options up to the user as options with defaults, rather than hard-coding in a certain choice, such as the method for optimization.

## Console messages

Use `message()` and `warning()` to communicate with the user in your functions. Please do not use `print()` or `cat()` unless it's for a `print.*()` method, as these methods of printing messages are harder for the user to suppress.

## DRY out your code

Attempt to follow the [Don't Repeat Yourself (DRY) principle](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself). This generally boils down to: keep your functions small. Even we can't claim to have perfectly DRYed code, but we are getting better at this :)

## Best practices for working with APIs

xxx

## Further guidance

The [`devtools` package](https://github.com/hadley/devtools) and it's wiki are an excellent resource for in-depth package development help.
