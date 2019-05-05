---
title: Package Managers
# tags: [formatting]
#keywords: popovers, tooltips, user interface text, glossaries, definitions
last_updated: May 5 2019
#summary: "You can add tooltips to any word, such as an acronym or specialized term. Tooltips work well for glossary definitions, because you don't have to keep repeating the definition, nor do you assume the reader already knows the word's meaning."
#sidebar: primary_sidebar
permalink: overview_package_managers.html
folder: overview
---

## yarn

[Yarn](https://yarnpkg.com/en/) is a package manager. Full documentation for yarn can be found [here](https://yarnpkg.com/en/docs).

While ruby gems are the standard for including libraries of ruby code into a project, they are not meant for including libraries that are used in all different types of web projects such as JavaScript or CSS frameworks.

Yarn works together with Ruby on Rails to take care of the management of these libraries to make sure they are always up to date. Ruby on Rails versions 5.1 and later support yarn 'out of the box'.

In the SafeTow Rails project, yarn is used to manage [jQuery](/assets_javascript#jquery) and [Bootstrap](/assets_stylesheets#bootstrap).

In the Rails project directory, there is a `yarn.lock` file that contains data about the packages being managed. The following code snippet is an example of the file contents.

```yml
bootstrap@^4.1.1:
  version "4.1.1"
  resolved "https://registry.yarnpkg.com/bootstrap/-/bootstrap-4.1.1.tgz#3aec85000fa619085da8d2e4983dfd67cf2114cb"

jquery@^3.3.1:
  version "3.3.1"
  resolved "https://registry.yarnpkg.com/jquery/-/jquery-3.3.1.tgz#958ce29e81c9790f31be7792df5d4d95fc57fbca"
```

A `node_modules` folder is also added to the root directory. For each package that is installed, a subfolder is added into `node_modules` that contains all of the necessary code.

In order for Ruby on Rails to import all of this code into the assets pipeline, we add the following line of code to `config/initializers/assets.rb`.

```ruby
Rails.application.config.assets.paths << Rails.root.join('node_modules')
```
