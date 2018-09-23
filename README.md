# Markdown inline HTML tag

This is a minimalist tool to process HTML files that contain a
`<markdown>` tag, rendering their content inline inside HTML.

This tool is a shell script pre-processor meant to render files before
publication and is suitable to use inside any POSIX system including
basic GNU or BSD implementations of tools like Grep and Awk, like
Apple/OSX and in chocolatey Windows scripts. It will likely perform
very well on both x86 and ARM platforms.

Markdown-inline-tag is derived from this other software
[Webnomad](https://github.com/dyne/webnomad). Here the script is
published externally to be more portable inside larger setups and
other web publishing software based on npm, yarn and similar tools.

## Requirements and portability

This tool requires the following dependencies to be installed:

```
zsh pandoc awk grep
```

Given the above components are installed, it is expected to run on any
platform: GNU/Linux, Apple/OSX and MS/Windows.

## Simple usage

Imagine having an `input.html` file containing plain HTML and then
using a special tag `<markdown>` which is not recognized by any
browser. In order to publish the file then the contents included
inside the tag would have to be transformed in HTML at the same place
inside the file (and the tag removed of course). This is exactly what
this tool does, for instance with the input file:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Mixing Markdown and HTML is fun</title>
	</head>
	<body>
		<div class="container">
			<markdown>
# This is a Title in markdown

This is a paragraph in markdown

- This
- Is a list
- of items
- in markdown

| This | Is  | A Table  | In Markdown |
| ---  | --- | ---      | ---         |
| And  | It  | Is Also  | In HTML     |
| Once | Is  | Rendered | By Pandoc   |
			</markdown>
		</div>
		<footer>This is a footer in HTML</footer>
	</body>
</html>
```

Will be tranformed into:

```html
<!DOCTYPE html>
<html>
	<head>
		<title>Mixing Markdown and HTML is fun</title>
	</head>
	<body>
		<div class="container">
<h1 id="this-is-a-title-in-markdown">This is a Title in markdown</h1>
<p>This is a paragraph in markdown</p>
<ul>
<li>This</li>
<li>Is a list</li>
<li>of items</li>
<li>in markdown</li>
</ul>
<table>
<thead>
<tr class="header">
<th>This</th>
<th>Is</th>
<th>A Table</th>
<th>In Markdown</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>And</td>
<td>It</td>
<td>Is Also</td>
<td>In HTML</td>
</tr>
<tr class="even">
<td>Once</td>
<td>Is</td>
<td>Rendered</td>
<td>By Pandoc</td>
</tr>
</tbody>
</table>
		</div>
		<footer>This is a footer in HTML</footer>
	</body>
</html>
```

To be run, our tool takes two arguments: input file and output file

```sh
markdown-inline-tag input.html output.html
```

launching it this way will not modify the input.html and will
overwrite the output.html without confirmation.

## NodeJS usage

The typical use of a NodeJs setup will be watching file changes and
live updating. The option `-w` runs markdown-inline-tag in a loop
refreshing results at every change of the input file. For instance
inside a `package.json` npm file one can add into the `scripts`
section:

```json
"scripts": {
	"index": "markdown-inline-tag -w views/index.html pub/index.html",
}
```
To live render the contents of `views/index.html` into
`pub/index.html`.

## Acknowledgements

Markdown-inline-tag is Copyright (C) 2012-2018 by Dyne.org foundation

Designed, written and maintained by Denis Roio <jaromil@dyne.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public
License along with this program. If not, see
http://www.gnu.org/licenses

