# Elixir Starter Toolbox 

One of my favorite parts about programming Elixir is the amount of tools that you can use and implement for have a 
better environment for code. 

Since you can run a `script` or open an `iEX` repl and try elixir, there are some tools that I found useful for any beginner.

## Code Editor

There are many good options for choose as `Code Editor`, I recommend spend some time choosing the best option based on the capabilities that this editor is giving to you for code, some of the most popular have good plugins:

#### Visual Studio Code

Maybe this is one of the most popular editors right now, you can install extensions for highlights ([VS Code Elixir](https://marketplace.visualstudio.com/items?itemName=mjmcloug.vscode-elixir)), code completion and debugger ([Elixir LS](https://marketplace.visualstudio.com/items?itemName=JakeBecker.elixir-ls)), open an `iEX`([iEX](https://marketplace.visualstudio.com/items?itemName=mbakerpdx.iex)) or run tests ([Elixir Test](https://marketplace.visualstudio.com/items?itemName=samuel-pordeus.elixir-test)).

#### Sublime Text

You can install plugins using the `Package Control`, there are packages for highlighting ([Elixir](https://packagecontrol.io/packages/Elixir)), or just for run the formatter ([Elixir Formatter](https://packagecontrol.io/packages/ElixirFormatter)).

#### VIM

You can open any elixir file, but if you want to set the syntax hightlights without a plugin, you can type `:set syntax=ruby` and the editor will render the file with highlights.  Also you can install plugins for the code highlights ([Vim Elixir](https://vimawesome.com/plugin/vim-elixir-sparks-fly)), implement mix commans ([Mix-Vim](https://vimawesome.com/plugin/mix-vim)), or just run the mix formatter ([Vim Mix Format](https://vimawesome.com/plugin/vim-mix-format)). Additionally you can use [tmux](https://github.com/tmux/tmux/wiki) for have a complete setup in your favorite terminal.

## Mix Tool

Your Elixir installation includes something called `Mix`, a build tool for manage an elixir project.

You can create a new project only with `mix new my_elixir_project`, run the project `mix run` or run the project inside a `iEX` typing `iex -S mix`, you can run the unit tests `mix test`, compile the project `mix compile`, and now you can package your project  with **mix release**. 

But `mix` have many tasks, you can know more typing `mix help`, and you will see tasks for **build and install an escript**, **delete generated files**, **download, clean, update and compile dependencies**. 

One of this useful commands is the formatter, this will format all files using useful standards. For this you have to run `mix format` in your project. 

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

