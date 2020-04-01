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

[Credo](https://github.com/rrrene/credo) it's an useful dependency focused on the code consistency. For have Credo inside your  project, you must add this `{:credo, "~> 1.2", only: [:dev, :test], runtime: false}` in your `mix.exs`.

With `$ mix credo` you will have some advices and suggestions for refactor your code based on an [style guide](https://github.com/rrrene/elixir-style-guide). 

## Automate Credo with Git Hooks

Use [git hooks](https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) is a great way for automate some tasks using **git**.

Writing a shell script as `pre push` hook allow us to run credo every time when you are pushing your commits to your remote repository and stop the operation if there are any issue to solve. 

Inside the mix project we need to create the file `.git/hooks/pre-push` with this content:

```
#!/bin/sh

mix credo
CREDO_RES=$?

if [ $CREDO_RES -ge 1 ]; then
  echo "======================================="
  echo "   Fix the credo suggestions, Push Operation Stopped!  "
  exit $CREDO_RES
fi
if [ $CREDO_RES -le 9 ]; then CREDO_RES=" $CREDO_RES"; fi
  echo "======================================="
  echo "There aren't Credo Issues, Push Operation Continue..."

echo ""
echo ""

# Finished
exit 0
```

## GitHub 

GitHub provides other tools for our elixir projects. 

There are a [GitHub Action](https://github.com/marketplace/actions/elixir-action) for run mix commands in your repository.

Another useful tool is the [dependabot](https://github.com/marketplace/dependabot-preview) for keep your dependencies updated. 

