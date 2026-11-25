---
name: coding-style
description: >-
  Personal coding style and Git commit message conventions.
  Use when writing, modifying, or reviewing code, or drafting Git commit messages.
metadata:
  upstream-title: "Franklin Yu’s Coding styles"
  upstream-url: "https://en.wikipedia.org/wiki/User:Franklin_Yu/Coding_styles"
  upstream-revision: "1386440123"
  upstream-revision-url: "https://en.wikipedia.org/w/index.php?title=User:Franklin_Yu/Coding_styles&oldid=1386440123"
  upstream-edited-on: "2026-11-18"
  synced-on: "2026-11-18"
---

# Coding styles

Unspecified details default to [Google style](https://google.github.io/styleguide/); fall back to [GitHub style](https://styleguide.github.com).

Full rationale, history, and citations are available in the [upstream revision](https://en.wikipedia.org/w/index.php?title=User:Franklin_Yu/Coding_styles&oldid=1386440123).

- Use [Shebang](<https://en.wikipedia.org/wiki/Shebang_(Unix)>) for executable scripts; remove file-type suffix.

- For instance-variable naming:

  - If a language has a clear owner (such as Apple for Objective-C or Microsoft for C#) that specifies a prefix or suffix, follow that convention and omit the redundant `this` or `self`.
    For C#, consider the [.NET Foundation](https://github.com/dotnet/runtime/blob/master/docs/coding-guidelines/coding-style.md) a de facto owner alongside Microsoft.
  - If there is no clear owner (notably C++), or the owner does not require a prefix or suffix (notably Java), use `this` or `self` instead of a prefix or suffix.

- For C/C++, shell scripts (POSIX, Bash, Zsh), Swift, CSS, and HTML: indent with tabs and align with spaces.

- For C/C++, the main function return with macros [`EXIT_SUCCESS` or `EXIT_FAILURE`](https://en.cppreference.com/w/c/program/EXIT_status).

- For structs and unions in C, use `struct message_body` instead of a `typedef` such as `Message`, following the [Linux kernel style](https://www.kernel.org/doc/html/latest/process/coding-style.html#typedefs).
  This rule does not apply to C++.

- For Python, fall back to [PEP 8](https://www.python.org/dev/peps/pep-0008/).

- For [systemd](https://en.wikipedia.org/wiki/Systemd) unit files, keep a space around the equal sign for readability.

- When creating command-line flags, use kebab-case like `--my-variable=3` and `--refresh-after-build=false`.
  If kebab-case is forbidden, prefer `snake_case` over `mixedCase` (lower camel case).

## Git commit message

Follow the Vim specification: first line is the summary, no longer than 50 characters; leave the second line empty; limit to 72 characters for other lines (except for long URL).
More rules:

- Use “Sentence case” for the summary, as if writing a sentence, but omit the period mark.
  Use an imperative sentence, such as “Delete foo”, instead of “Deleting foo” or “Deletes foo”.

- Use Markdown where it helps, and keep the body readable as plain text.
  Apply the same 72-column limit and long URL exception to Markdown commit messages.

### Git trailers

Use [trailers](https://git-scm.com/docs/git-interpret-trailers/2.32.0) for commit metadata.

- If the change is trivial (re-format, fix typo, etc.), add `Minor-commit: true`.

- If the body uses markup, add a `Format` trailer with the lowercase identifier defined by [GitHub Markup](https://github.com/github/markup/blob/master/lib/github/markup.rb), such as `markdown`, `asciidoc`, `rst`, or `rdoc`.
  Examples: `Format: markdown` for Markdown and `Format: rst` for reStructuredText.

- For commits created by an AI coding assistant, add an `Assisted-by` trailer naming the tool, such as `Assisted-by: Codex`, `Assisted-by: Claude Code`, or `Assisted-by: Antigravity`.

- Record the corresponding session in `Codex-Session`, `Claude-Session`, or `Antigravity-Session`.
  Use the complete native session identifier, including the full UUID when applicable.

### Agent commit guidance (maintained locally)

Before creating or amending a commit as an agent, read the [local commit guidance](references/agent-commits.md).

## Java

- Prefer underscores to separate words in package names, such as `google.app_engine`, for readability.

- When there are more than 10 non-static imports, prefer separating JDK imports from imports for other dependencies.

## JavaScript/TypeScript

- For plain JavaScript that are highly unlikely to go into Google, use [StandardJS](https://standardjs.com) instead of Google style.
  Use Google style for all TypeScript.

- Avoid built-in `window.prompt()`, `window.confirm()` and `window.alert()`.

## Makefile

- [implicit rules](https://www.gnu.org/software/make/manual/html_node/Implicit-Rules.html)

- [auto-dependency generation](https://make.mad-scientist.net/papers/advanced-auto-dependency-generation/)

- Avoid `@` suppressing [recipe echoing](https://www.gnu.org/software/make/manual/html_node/Echoing.html): it provides debugging information such as variable expansion.
  Normally leave suppression to the user through `-s`/`--silent`.
  Prefer [`--debug=basic`](https://www.gnu.org/software/make/manual/html_node/Options-Summary.html#index-_002d_002ddebug) over replacing a target's recipe echoing with manual `@echo` messages.

## Markdown

Write each sentence of a prose paragraph on its own source line.
Use ordinary newlines between sentences and a blank line between paragraphs.

## Ruby

- Use the Robocop style for [Ruby](https://github.com/rubocop-hq/ruby-style-guide) and [Rails](https://github.com/rubocop-hq/rails-style-guide); fall back to Google, then GitHub style.

- [RSpec guides](https://www.betterspecs.org)

- Fix major version of gems in `Gemfile` (with `~>`).

## shell scripts

“All shells” below means Bash, Zsh, [Dash](https://en.wikipedia.org/wiki/Almquist_shell#dash), and [BusyBox](https://en.wikipedia.org/wiki/BusyBox).

- [override] Omit unnecessary braces for parameter expansion, such as `echo "value=$var"` and `PATH="$PATH:/my/path"`, instead of `echo "value=${var}"` and `PATH="${PATH}:/my/path"`.

- For [`set`](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#set) builtin, use the `-o` version with long names instead of short names like `-e`.
  Recommended options are `errexit` and `nounset`.
  Non-POSIX [`pipefail`](https://www.gnu.org/software/bash/manual/html_node/The-Set-Builtin.html) is also recommended when in Bash/Zsh.

- Use kebab-case for aliases.
  This is not POSIX, but it is supported in all shells listed above.

- [override] Use kebab-case for functions in Bash/Zsh.
  They are not supported in Dash or BusyBox.

- When a command provides multiple versions of the same option (such as `-q`/`--brief` in GNU [Diff](https://en.wikipedia.org/wiki/Diff)), avoid the single-letter one.
  Optimize for readers, instead of authors; short form is good for interactive sessions.

- Prefer `--key=value` over `--key value` to make the binding explicit.
  For long flags, prefer double dash like `--flag` over single dash like `-flag`; reserve single dash for short forms when a long form is unavailable or for interactive use.

- Keep one space before, but none after, I/O redirection operators: `command <file1 >file2`.
  The operator binds to the file path.

- [override] For Zsh, do not quote a single variable like `$var` into `"$var"`, since Zsh doesn’t expand them like Bash does.

### wrapping long commands

Prefer avoiding backslashes by breaking after `|`, which permits continuation on the next line.
The same applies to [`&&` and `||`](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18_09_03).

Keep complete commands together on a line when they fit.
Move a command that does not fit to the next line rather than putting only its first few words on the previous line.
When a command itself needs a backslash continuation, indent its continuation an additional level.

```bash
command1 | command2 | command3 | command4 |
  command5 |
  command6 --with --many=flags "and arguments" |
  command7 --config=/usr/share/some-config.yaml \
    --input="$HOME/.local/share/some-data.json"
  command8
```

### use shell features instead of helper commands

Avoid [UUoC](<https://en.wikipedia.org/wiki/Cat_(Unix)#Useless_use_of_cat>).
In Bash/Zsh, use [here strings](https://www.gnu.org/software/bash/manual/html_node/Redirections.html#Here-Strings) instead of piping a useless `echo`:

```bash
foobar <<<'input text'
```

### define functions

When POSIX compatibility is not needed, use the `function` keyword to avoid the function name being replaced by an alias.
Prefer omitting the optional parentheses:

```bash
function foo {
  # body
}
```
