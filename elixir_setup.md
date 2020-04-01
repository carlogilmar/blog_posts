# Elixir Starter Toolbox 

One of my favorite parts of the **Elixir ecosystem** is the tooling support that let's you customize the best environment for coding. 

## The Programming Language

Some of the most useful tooling comes with Elixir. Possibly the most useful tool for a beginner is Elixir's REPL (read-eval-print loop) which can run easily with `$ iex`. This allows us to evaluate small chunks of Elixir code or explore the documentation with the [IEx helpers](https://elixirschool.com/en/lessons/basics/iex-helpers/).

Another useful tip is use Elixir Scripts, files ending `.exs`,  to experiment with larger pieces of code. These files can be quickly evaluated in the terminal with `$ elixir file.exs` .

In addition tooling included with Elixir there is a wonderful variety of tools creating by others for us to use. 

## The Code Editor

There are many good options when picking an editor. It's likely your favorite editor has support for Elixir but not all support is equal. Below are some editors with standout Elixir support.

#### Visual Studio Code

The most popular editor in the Elixir community, with extensions for [syntax highlight](https://marketplace.visualstudio.com/items?itemName=mjmcloug.vscode-elixir), code completion and debugger support through [Elixir LS](https://marketplace.visualstudio.com/items?itemName=JakeBecker.elixir-ls), and in-editor support for running IEx or executing tests.

Visual Studio Code is a solid choice if you don't already have a favorite.

#### Sublime Text

With Package Control add [syntax highlighting](https://packagecontrol.io/packages/Elixir) or enabling the [Elixir Formatter](https://packagecontrol.io/packages/ElixirFormatter) is easy.

#### VIM

If you're already using VIM there's a number of great plugins to consider. [Syntax highlighting](https://github.com/elixir-editors/vim-elixir) is a must. Code completion, documentation, IEx support, Mix integration, and more can be added [alchemist.vim](https://github.com/slashmili/alchemist.vim).

## Mix Tool

In addition to the wonderful IEx tool included with Elixir another tool is included for handling the nitty-gritty of Elixir: **Mix**.

With Mix it is possible to create new projects easily with `$ mix new my_elixir_project`, compile our code with `$ mix compile`, execute tests `$ mix test`, run our project with `$ mix run` , and even release production code with `$ mix release`.

Another command to keep in mind that is useful is `$ mix format` which runs the official code formatter on our project. 

There are _many more_ things Mix can do. It is possible to see the list with `$mix help`.

## Credo

Credo it's an [elixir dependency](https://github.com/rrrene/credo) for check code consistency. When you run Credo inside your project you will see: consistency issues, refactoring opportunities, warnings, improves in software design and code readability. This will help you to improve your code consistency, you can know more about in the [style guide](https://github.com/rrrene/elixir-style-guide) implemented in Credo. 

I consider that Credo must be in the starter setup because his recommendations are a good thing not only for have a standar code style, you can learn how to write better code: include `@moduledoc` in every module, set the correct spaces, don't missing `TODO` comments, etc.

## Automate Credo 

I use to initialize a git repository in every software project. This allow me to take advantage of the [git hooks](https://www.google.com/search?q=git+hooks&oq=git+hooks&aqs=chrome..69i57j0l6j69i60.3675j0j1&sourceid=chrome&ie=UTF-8), I use to implement a `Pre Push Git Hook` with `Credo`, a shell script for run `mix credo` before to push the changes to the remote repository, if `Credo` have any issue, the push action will be rejected until there aren't any issue. 

For implement this, you'll need to have a file with this path `.git/hooks/pre-push` inside your `.git` directory

```
#!/bin/sh

mix credo
CREDO_RES=$?

if [ $CREDO_RES -ge 1 ]; then
  echo "======================================="
  echo "   Fix the credo suggestions  "
  exit $CREDO_RES
fi
if [ $CREDO_RES -le 9 ]; then CREDO_RES=" $CREDO_RES"; fi
  echo "======================================="
  echo "There aren't Credo Issues, Push Continue.."
  echo "======================================="

echo ""
echo ""

# Finished
exit 0
```

## GitHub 

Recently GitHub launch the GitHub Actions for automate workflows, if you're using this, there are a GitHub Action for run mix commands in your repository: [Elixir Action](https://github.com/marketplace/actions/elixir-action)

And if you want to have your dependencies updated, you can try the [dependabot](https://github.com/marketplace/dependabot-preview), this will check your dependencies versions and if he found any dependencie to update, he will open a Pull Request with the most updated version in your repository.

