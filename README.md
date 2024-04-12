<!-- deno-fmt-ignore-file -->

deno-task-hooks
===============

[![JSR][JSR badge]][JSR]
[![GitHub Actions][GitHub Actions badge]][GitHub Actions]

This package provides a simple way to run [Deno tasks] as [Git hooks].  You can
define Git hooks in your *deno.json* file and share them with your team.

[JSR]: https://jsr.io/@hongminhee/deno-task-hooks
[JSR badge]: https://jsr.io/badges/@hongminhee/deno-task-hooks
[GitHub Actions]: https://github.com/dahlia/deno-task-hooks/actions/workflows/main.yaml
[GitHub Actions badge]: https://github.com/dahlia/deno-task-hooks/actions/workflows/main.yaml/badge.svg


How to set up
-------------

First of all, you need to add `hooks:install` task to your *deno.json* file:

~~~~ json
{
  "tasks": {
    "hooks:install": "deno run --allow-read=deno.json,.git/hooks/ --allow-write=.git/hooks/ jsr:@hongminhee/deno-task-hooks"
  }
}
~~~~

This `hooks:install` task will install the hooks defined in your *deno.json*
file to your *.git/hooks* directory.  Let your team members run this task
immediately after cloning your repository.

Then, you can define your Git hooks in your *deno.json* file.  All hooks are
prefixed with `hooks:` and followed by the hook name (which is kebab-cased).
For example, to define a `pre-commit` hook, you can add the following task:

~~~~ json
{
  "tasks": {
    "hooks:pre-commit": "deno check *.ts && deno lint"
  }
}
~~~~

Then, install the hooks by running the following command:

~~~~ sh
deno task hooks:install
~~~~

Now, the `pre-commit` hook is installed to your *.git/hooks* directory.  That's
it!  You can now run `git commit` and see your `pre-commit` hook in action.

[Deno tasks]: https://docs.deno.com/runtime/manual/tools/task_runner
[Git hooks]: https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks
