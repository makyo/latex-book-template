# LaTeX Book Template

A template for generating a book in LaTeX.

## Requirements

* [`pandoc`][pandoc]
* `xelatex` (included in TeXLive)
* `make`
* (Optional) [Gentium Plus](https://software.sil.org/gentium/download/) font

## Getting started

This repository is a template for generating a trade paperback book. It creates a PDF that one can send to a printer for final production. As an additional feature, it generates a (very basic) EPub3 file to get you started on an ebook version.

To get going with this, copy the files in this repository to where you wish to work, modify the `includes/variables.tex` file to populate the title, author, and other information, add your content, and then run it using the following commands.

## Running

There are several `make` targets available to you, depending on what you want to be generated:

* `make plain` runs `xelatex` once
* `make toc` runs `xelatex` twice. This is needed to regenerate table of contents and references with page numbers.
* `make draft` generates a watermarked file for proofreading
* `make proof` generates a full proofing file with frame and crop marks, a draft watermark, and on letter paper for margins
* `make final` generates a final draft --- this is equivalent to `make toc`, except that it resets all draft stuff that may be left behind.
* `make ebook` generates an EPub3 file. This will be exceedingly plain and not include any graphics, so you'll need to use something like [Calibre][calibre] to generate a final product, but this will get you started.

Additionally, there are a few targets which probably won't be used directly, but may be helpful:

* The `engage-letter` target outputs to letter-size paper from the default trade paperback size. This only controls the paper size, not the layout size, though, so you will get a trade page centered in a letter page.
* The `reset` target resets all switchable options (draft, letter paper, framing/crop marks) to production values.

## Adding content

First things first, modify the `includes/variables.tex` file to contain the proper title, author, and additional information.

You may add content directly in the content directory as `*.tex` files, or you may write in Markdown in the `src/content` directory. If you wish to do this, each file in that directory will be transpiled from Markdown into LaTeX using [pandoc][pandoc]. To generate these files, run `make content`.

You may add assets such as images in the `assets` directory to be included in your content. Note that file paths such as those used in `\includegraphics` should be relative to `book.tex` (that is, don't write `\includegraphics{../assets/stuff.png}`, but instead `\includegraphics{assets/stuff.png}`).

Once you have your content in your files modify `book.tex` to include each file in `content` with `\input{}` commands. The file in this repository includes example includes, and you'll probably want to remove those.

You'll likely want to edit `includes/copyright.tex` to match your needs.

## Customization

The output of this template is deliberately bland, and is intended to be customaized.

* Customize final page and layout size in `includes/_geometry-trade.tex`. This includes sensible defaults for margins and such already.
* Customize fonts in `includes/font.tex`
* Add hyphenation rules to `includes/hyphenation.tex`
* Customize page layout (header, footer, etc) in `includes/pagelayout.tex`
* Set a custom section divider in `includes/secdiv.tex`. This redefines the `\rule` command to be something more appealing. This is optional, though, and the `\input{includes/secdiv}` command in `book.tex` can be removed to restore defaults.
* Customize your title and pretitle pages in `includes/title.tex` and `includes/pretitle.tex`

[pandoc]: https://pandoc.org
[calibre]: https://calibre-ebook.com/
