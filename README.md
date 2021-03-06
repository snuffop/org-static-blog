![melpa badge](http://melpa.org/packages/org-static-blog-badge.svg) ![melpa stable badge](http://stable.melpa.org/packages/org-static-blog-badge.svg)

ORG-STATIC-BLOG
===============

Static blog generators are a dime a dozen. This is one more, which
focuses on being simple. All files are simple org-mode files in a
directory. The only requirement is that every org file must have a
`#+TITLE` and a `#+DATE`, and optionally, `#+FILETAGS`.

This file is also available from marmalade and melpa-stable.

Set up your blog by customizing org-static-blog's parameters, then
call `M-x org-static-blog-publish` to render the whole blog or
`M-x org-static-blog-publish-file filename.org` to render only only
the file `filename.org`.

Above all, I tried to make org-static-blog as simple as possible.
There are no magic tricks, and all of the source code is meant to be
easy to read, understand and modify.

For org-static-blog, a blog consists of six parts:
- Blog posts contain individual entries. Every org file in
  `org-static-blog-posts-directory` is one blog post. Each blog post
  is rendered as its own HTML page.
- The index page contains the last few blog posts on a single page.
  The number of entries on the index page can be customized using
  `org-static-blog-index-length`.
- The archive page lists the publishing dates and headlines of every
  blog post.
- The RSS feed is a machine-readable XML file that contains every blog
  post. It is not meant to be consumed by humans. Instead RSS readers
  can use the RSS feed to aggregate entries from multiple blogs.
- Drafts are rendered like regular blog posts, but are not included in
  the index, the archive, or the RSS feed.
- Each blog post can be tagged, and each tag links to a page that
  lists all other posts of the same tag. Additionally, a tag overview
  page is created that lists the publishing dates and headlines of
  every blog post, sorted by tags. This feature is only enabled if you
  set `org-static-blog-enable-tags` to `t`.

Every HTML page in org-static-blog can be customized in the following
ways:
- The contents of `org-static-blog-page-header` are inserted into the
  `<head>` of every page. Use this to include custom CSS and
  JavaScript for your blog.
- The contents of `org-static-blog-page-preamble` is inserted just
  before the content of every page. This is a good place to put the
  header or menus for your blog.
- The contents of `org-static-blog-page-postamble` is inserted just
  after the content of every blog entry, but not in the index page and
  the archive. This is where you can include copyright notices or
  comment boxes.
- The return values of `org-static-blog-post-preamble` and
  `org-static-blog-post-postamble` are prepended and appended to every
  blog post. If you want to change the formatting of dates, titles, or
  the tag list, overwrite these functions.

If you want to activate a few convenience key bindings, add
`(add-to-list 'auto-mode-alist (cons (concat org-static-blog-posts-directory ".*\\.org\\'") 'org-static-blog-mode))`
to your *init.el*. These key bindings are:
- `C-c C-f`/`C-c C-b` to open next/previous post.
- `C-c C-p` to open the matching published HTML file of a post.
- `C-c C-n` to create a new blog post.


If you have questions, if you find bugs, or if you would like to
contribute something to org-static-blog, please open an issue or pull
request on GitHub.

Finally, I would like to remind you that I am developing this project
for free, and in my spare time. While I try to be as accommodating as
possible, I can not guarantee a timely response to issues. Publishing
Open Source Software on GitHub does not imply an obligation to *fix
your problem right now*. Please be civil.

Examples
--------

`org-static-blog` was used to render [bastibe.de/][blog]. Have
a look at my [init.el][init] and the [repository][repo] for the blog
itself to see an example of how to use `org-static-blog` in practice.

Other org-journal blogs:
- [https://zngguvnf.org/][zngguvnf.org]
- [https://matthewbauer.us/blog/][matthewbauer.us/blog/]
- Please open a pull request to add your blog, here!

[blog]: http://bastibe.de
[init]: https://github.com/bastibe/.emacs.d/blob/master/init.el#L670
[repo]: https://github.com/bastibe/bastibe.github.com
[zngguvnf.org]: https://zngguvnf.org/
[matthewbauer.us/blog/]: https://matthewbauer.us/blog/

Known Issues
-----------

- Org-static-blog is a pure static site generator. As such, it does
  not include comments. However, you can easily include services like
  Disqus to do this for you.
- You can have hosting services like GitHub auto-render you blog every
  time you commit using continuous integration tools like Travis CI.
  An example of how to do this has been gracefully provided
  by [zngguvnf](https://gitlab.com/_zngguvnf/org-static-blog-example).
- Individual blog entries are only re-rendered if no current HTML file
  is available (i.e. the org file is older than the HTML file). If you
  want to forcibly re-render an entry, delete the HTML file.

Changelog
---------

- 2018-03-17 (v1.0.4): Massive speed up of org-static-blog. A
  re-render with one changed file used to take about a second per
  post, and now takes about a second total.
- 2018-03-21 (v1.1.0): Tags.
  Each post can now have tags (using `#+tags:`). If you enable
  `org-static-blog-enable-tags`, tags are included in each post,
  tag-index pages are generated for each tag, and a tag archive
  is generated for all tags.
- 2018-03-23 (v1.1.1): Tags.
  Deprecated `#+tags:` in favor of `#+filetags:`, which is the
  correct way of setting file-wide tags in org-mode.
  (Thank you, Kaushal Modi!)
- 2018-04-19 (v1.2.0): HTML5
  Org-static-blog now outputs valid HTML5 instead of XHTML. This makes
  the resulting HTML cleaner, but shouldn't impact your styles. Also,
  you can now customize your content language by setting
  `org-static-blog-langcode` and the HTML output has been fixed in a few
  places.
  (Thank you, Michael Cardell Widerkrantz!)

LICENSE
-------

Copyright 2015, Bastian Bechtold

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are
met:

1. Redistributions of source code must retain the above copyright
   notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the
   distribution.

3. Neither the name of the copyright holder nor the names of its
   contributors may be used to endorse or promote products derived
   from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
"AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
