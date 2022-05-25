Hi!

I have a section of site: `/about`.
In this section I wish to have a custom layout that consists of specific section's menu.
So each single page in this section should inherit this layout.
Moreover, each page of this section has a specific markup (HTML) and its "content" file usually is empty.

```
/content
  /about
    /_index.md
    /contacts.md    <- Empty content. Should use _default/baseof -> about/single -> about/contacts
    /job.md         <- Empty content. Should use _default/baseof -> about/single -> about/job
/layouts
  /_default
    /_baseof.html
    /single.html
  /about
    /single.html    <- Defines common `/about` layout and section menu
    /contacts.html  <- Custom HTML for `/about/contacts` page
    /job.html       <- Custom HTML for `/about/job` page
```

layouts/_default/baseof.html

```
<head>...</head>
<h1>Site title</h1>
<body>{{ block "main" . }}{{ end }}</body>
```

layouts/about/single.html

```
{{- define "main" -}}
<h2>About us</h2>
{{ block "custom-content" . }}{{ end }}
{{- end -}}
```

layouts/about/contacts.html

{{- define "custom-content" -}}
There is a contact list here
{{- end -}}

As a result I expect the following at `/about/contacts`

```
<h1>Site title</h1>
<h2>About us</h2>
There is a contact list here
```
