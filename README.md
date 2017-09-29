# Front-End Cheat Sheet

### Design Patterns:

Design patterns are advanced object-oriented solutions to commonly occurring software problems.  Patterns are about reusable designs and interactions of objects.  Each pattern has a name and becomes part of a vocabulary when discussing complex design solutions.

The 23 Gang of Four (GoF) patterns are generally considered the foundation for all other patterns. They are categorized in three groups: Creational, Structural, and Behavioral

 
| Creational Patterns        |    Design patterns that deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.    |
| ------------- |:-------------:|
| Prototype     |   A fully initialized instance to be copied or cloned |
| Singleton   | A class of which only a single instance can exist   |



| Structural Patterns|    Design Patterns that ease the design by identifying a simple way to realize relationships between entities.    |
| ------------- |:-------------:|
| Prototype     |   A fully initialized instance to be copied or cloned |
| Singleton   | A class of which only a single instance can exist   |
 
 * Prototype	A fully initialized instance to be copied or cloned
 * Ctrl+Shift+S / Cmd+Shift+S to choose to save as Markdown or HTML
 * Drag and drop a file into here to load it
 * File contents are saved in the URL so you can share files


I'm no good at writing sample / filler text, so go write something yourself.

Look, a list!

 * foo
 * bdjdhdh
 * baz

And here's some code! :+1:

```javascript
$(function(){
  $('div').html('I am a div.');
});
```

This is [on GitHub](https://github.com/jbt/markdown-editor) so let me know if I've b0rked it somewhere.


Props to Mr. Doob and his [code editor](http://mrdoob.com/projects/code-editor/), from which
the inspiration to this, and some handy implementation hints, came.

### Stuff used to make this:

 * [markdown-it](https://github.com/markdown-it/markdown-it) for Markdown parsing
 * [CodeMirror](http://codemirror.net/) for the awesome syntax-highlighted editor
 * [highlight.js](http://softwaremaniacs.org/soft/highlight/en/) for syntax highlighting in output code blocks
 * [js-deflate](https://github.com/dankogai/js-deflate) for gzipping of data to make it fit in URLs
