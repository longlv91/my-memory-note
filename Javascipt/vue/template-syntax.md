# Template Syntax

## Text

The most basic form of data binding is text interpolation using the “Mustache” syntax (double curly braces):

```
<span>Message: {{ msg }}</span>
```

You can also perform one-time interpolations that do not update on data change by using the v-once directive, but keep in mind this will also affect any other bindings on the same node:

```
<span v-once>This will never change: {{ msg }}</span>
```

## Raw HTML

The double mustaches interprets the data as plain text, not HTML. In order to output real HTML, you will need to use the v-html directive:

```
<p>Using mustaches: {{ rawHtml }}</p>
<p>Using v-html directive: <span v-html="rawHtml"></span></p>
```