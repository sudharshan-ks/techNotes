# Template
1. With template you've an infinite power
2. Jinja2 templating is used
3. Templating happens on the control node and the task is sent to the managed node for execution.
```
$ cat template/settings.conf 
<..snip..>
hostname: {{hostname}}
<..snip...>


```