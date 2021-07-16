---
title: "Attachments"
linkTitle: "Testing Shortcode Attachments"
weight: 1
icon: fas fa-paperclip
tags: ["Shortcode", "Attachments"]
projects: ["Docsy"]
description: >
  Testing Shortcode Attachments
resources:
- src: '**.pdf'
  name: pdf-file-name-:counter
  title: pdf-file-title-:counter
  params:
    description: "This ist the description of all PDF files."
  
---

Shortcode to show a list of downloadable page resources resp. files in a folder.

| Parameter        | Default    | Description  |
| ---------------- |------------| ------------|
| title | (T "shortcode_attachments") | The title of the box with the attachments. (The default value is a language specific variable.)
| icon |  "fas fa-paperclip"| Code for FontAwesome icon left from the title.
| folder | | If empty the page resources are used for the file list. If set a specific folder relativ to the current page can be used for generating a file list.
| recursive |  true | If true als files in subfolders will be found (only if the parameter `folder` is used).
| filter | "." | RegEx filter on the filename relativ to the current page.
| match | "**" | Glob pattern for filtering __page resources__.
| class | | Additional HTML class for the `<div>` containing the box with the attachments.
| num_fmt |  | "- , ."| Parameter for formating file size (see [Hugo docs](https://gohugo.io/functions/numfmt/)).
| num_fmt_del | " | " "| Corresponding delimiter for parameter for formating file size (see [Hugo docs](https://gohugo.io/functions/numfmt/)).
| empty_list |  "No attachments found." | Shown message if file list is empty.

Some examples for different parameter settings for the shortcode `attachmeents`:

## Pure version without any parameter

The pure shortcode `{{</* attachments /*/>}}` displays __all__ page resources of a page bundle. As visible Text for the links the resource parameter `title` is used. Default `title` value is the filename (relative to the owning page). Can be set in front matter.
 If set, also the resource parameter `params.description` get displayed under the link. All the resource parameter can be set by [corresponding page’s front matter](https://gohugo.io/content-management/page-resources/#page-resources-metadata "Link to official Hugo docs").

This is the front matter of the current page:

```yaml
title: "Attachments"
linkTitle: "Testing Shortcode Attachments"
weight: 1
icon: fas fa-paperclip
tags: ["Shortcode", "Attachments"]
projects: ["Docsy"]
description: >
  Testing Shortcode Attachments
resources:
- src: '**.pdf'
  name: pdf-file-name-:counter
  title: pdf-file-title-:counter
  params:
    description: "This ist the description of all PDF files."
```

{{< attachments />}}

### Pure version with inner content

Also a inner content will be shown within the attachments box:
```md
{{</* attachments */>}}
#### An inner Headline

Some inner text.
{{</* /attachments */>}}
```

{{< attachments >}}
#### An inner Headline

Some inner text.
{{< /attachments >}}

## Using spezific Folder

Especially for __none page bundles__ (not `index.md` or `_index.md`) it is also possible to set a specific subfolder for attachments `{{</* attachments folder="files" title="Files in folder" /*/>}}`:

{{< attachments folder="files" title="Files in folder" />}}

## Using filter options

The resulting file list can be filtered by the options `filter` (by using [RegEx](https://gohugo.io/functions/findre/ "Docs from used Hugo function for RegEx filtering.") on the filename relative to the current page). 

{{< attachments title="Filtered page resources for jpg files" filter=".+\.(?i)(jpg|jpeg)$" />}}

{{< attachments folder="/" title="Filtered all files in folder for 'doc'" filter="doc" >}}
Also the file `document.pdf` get listed, because it begins with "doc".
{{< /attachments >}}

If displaying page resources alternatively the parameter `match` can get used as file list filter. __But [Glob pattern](https://gohugo.io/content-management/page-resources/#pattern-matching "Link to pattern examples") has to be used and the name of the page resource instead of the file name get filtered!__

{{< attachments title="Filtered page resources for 'files/*'" match="files/*" />}}
