# Highlight.js

Highlight.js highlights syntax in code examples on blogs, forums and,
in fact, on any web page. It's very easy to use because it works
automatically: finds blocks of code, detects a language, highlights it.

Autodetection can be fine tuned when it fails by itself (see "Heuristics").


## Installation and usage

The download package includes the file "highlight.pack.js" which is a full
compressed version of the library intended for use in production. All
uncompressed source files are also available, feel free to look into them!

The script is installed by linking to a single file and making a single
initialization call:

    <script type="text/javascript" src="highlight.pack.js"></script>
    <script type="text/javascript">
      hljs.initHighlightingOnLoad();
    </script>

Also you can replace TAB ('\x09') characters used for indentation in your code
with some fixed number of spaces or with a `<span>` to give them special
styling:

    <script type="text/javascript">
      hljs.tabReplace = '    '; // 4 spaces
      // ... or
      hljs.tabReplace = '<span class="indent">\t</span>';

      hljs.initHighlightingOnLoad();
    </script>

The script looks in your page for fragments `<pre><code>...</code></pre>`
that are traditionally used to mark up code examples. Their content is
marked up by logical pieces with defined class names.


### Custom initialization

If you use different markup for code blocks you can initialize them manually
with `highlightBlock(code, tabReplace)` function. It takes a DOM element
containing the code to highlight and optionally a string with which to replace
TAB characters.

Initialization using, for example, jQuery might look like this:

    $(document).ready(function() {
      $('pre code').each(function(i, e) {hljs.highlightBlock(e, '    ')});
    });

If your code container relies on `<br>` tags instead of line breaks (i.e. if
it's not `<pre>`) pass `true` into third parameter of `highlightBlock`:

    $('div.code').each(function(i, e) {hljs.highlightBlock(e, null, true)});


### Styling

Elements of code marked up with classes can be styled as desired:

    .comment {
      color: gray;
    }

    .keyword {
      font-weight: bold;
    }

    .python .string {
      color: blue;
    }

    .html .atribute .value {
      color: green;
    }

Highlight.js comes with several style themes located in "styles" directory that
can be used directly or as a base for your own experiments.

For full reference list of classes see [classref.txt][cr].

[cr]: http://github.com/isagalaev/highlight.js/blob/master/classref.txt

## Node.js

### Installation

Use `npm` package manager

    npm install highlight

### Usage

Include syntax highlighter

    var hl = require("highlight").Highlight;

highlight code

    html = hl("for(var i=0;i<10;i++)alert(i);");

use special tab replacing string (default is 4 spaces)

    html = hl(code_string, "<span>  </span>");

convert code only between &lt;code&gt; blocks (leaves everything else as is) - especially useful if used together with converted [Markdown](/andris9/node-markdown) syntax that includes &lt;code&gt; blocks.

    html = hl("<p>PHP:</p><code><?php echo 'Hello world!';?></code>", false, true);

## Export

File export.html contains a little program that allows you to paste in a code
snippet and then copy and paste the resulting HTML code generated by the
highlighter. This is useful in situations when you can't use the script itself
on a site.


## Heuristics

Autodetection of a code's language is done using a simple heuristic:
the program tries to highlight a fragment with all available languages and
counts all syntactic structures that it finds along the way. The language
with greatest count wins.

This means that in short fragments the probability of an error is high
(and it really happens sometimes). In this cases you can set the fragment's
language explicitly by assigning a class to the `<code>` element:

    <pre><code class="html">...</code></pre>

You can use class names recommended in HTML5: "language-html",
"language-php". Classes also can be assigned to the `<pre>` element.

To disable highlighting of a fragment altogether use "no-highlight" class:

    <pre><code class="no-highlight">...</code></pre>


## Meta

- Version: 6.0
- URL:     http://softwaremaniacs.org/soft/highlight/en/
- Author:  Ivan Sagalaev (<Maniac@SoftwareManiacs.Org>)

For the license terms see LICENSE files.
For the list of contributors see AUTHORS.en.txt file.
