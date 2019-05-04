---
layout: post
title: Converting markdown to HTML with Github's CMark-GFM library in C + How to use extensions!
date: 2018-10-26 22:25
summary: Like many C libraries, CMark-GFM, does not have the most clear documentation. In this article we will learn how to use it.
categories: Dev-Tutorials
---

Today, I was working on [MarkdownPanda](https://github.com/Open-App-Library/markdownpanda), a bi-directiona HTML/Markdown conversion library that will be very important to [Vibrato Notes](https://vibrato.app).

With MarkdownPanda, I have gone through quite the number of Markdown parsers. I started my decision with Sundown and Discount. Then decided to go with Hoedown. I was happy with Hoedown up until the point where I noticed super strange behavior in my unit tests where previous markdown->HTML operations would concatenate onto new ones...Super weird and just made me want to find something new. Came across CMark and found it absolutely perfect..Until I realized tables and strikethroughs were not implemented. **And then I found Github's own CMark-GFM**.

At a surface level, the library is super simple and hardly any different than CMark.

## Example Program

```c
#include <stdio.h>
#include <string.h>
#include <cmark-gfm.h>

int main()
{
  char *markdown = "# Welcome";
  char *html = cmark_markdown_to_html(markdown, strlen(markdown), CMARK_OPT_DEFAULT);

  printf("%s", html);
  free(html);

  return 0;
}
```

Easy, right? Must be smooth sailing from here! Well..we do have a bit of a problem. Tables and strikethroughs are not supported by default. There are also [other](https://github.com/github/cmark-gfm/tree/master/extensions) extensions you may find useful.

## Using extensions

In order to use extensions you must first make sure to link against `libcmark-gfm-extensions`. It is an additional library that is created while building CMark-GFM.

Here is an example program that uses markdown extensions:

```c
#include <stdio.h>
#include <string.h>
#include <cmark-gfm.h>
#include <cmark-gfm-core-extensions.h>

// This is a function that will make enabling extensions easier later on.
void addMarkdownExtension(cmark_parser *parser, char *extName) {
  cmark_syntax_extension *ext = cmark_find_syntax_extension(extName);
  if ( ext )
    cmark_parser_attach_syntax_extension(parser, ext);
}

// A function to convert HTML to markdown
char *to_html(char *markdown_string)
{
  int options = CMARK_OPT_DEFAULT; // You can also use CMARK_OPT_STRIKETHROUGH_DOUBLE_TILDE to enforce double tilde.

  cmark_gfm_core_extensions_ensure_registered();

  // Modified version of cmark_parse_document in blocks.c
  cmark_parser *parser = cmark_parser_new(options);

  ///////////////////////
  /// Add extensions here
  ///////////////////////
  addMarkdownExtension(parser, "strikethrough");
  addMarkdownExtension(parser, "table");

  cmark_node *doc;
  cmark_parser_feed(parser, markdown_string, strlen(markdown_string));
  doc = cmark_parser_finish(parser);
  cmark_parser_free(parser);

  // Render
  char *html = cmark_render_html(doc, options, NULL);
  cmark_node_free(doc);

  return html
}

// MAIN FUNCTION
int main()
{
  char *markdown = "# Welcome";
  char *html = to_html(markdown);

  printf("%s", html);
  free(html);

  return 0;
}
```

Hope this saved you some time! You can check out how we implemented this in MarkdownPanda by viewing [markdownpanda_md2html.c](https://github.com/Open-App-Library/markdown-panda/blob/master/src/markdownpanda_md2html.c).

If you enjoyed, feel free to [browse our open-source software](/projects/).
