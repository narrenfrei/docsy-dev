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
| title | Attachments | The title of the box with the attachments. (The default value is the language specific variable `sc_attachments`.)
| icon |  fas fa-paperclip| Code for FontAwesome icon left from the title.
| folder | | If empty the page resources are used for the file list. If set a specific folder relativ to the current page can be used for generating a file list.
| recursive |  true | If true als files in subfolders will be found (only if the parameter `folder` is used).
| exclude | .md,.markdown | Exclude Files with specific extenstion. By default markdown files are excluded, because they get renderd to an html file.
| filter | . | RegEx filter on the filename relativ to the current page.
| match | ** | Glob pattern for filtering __page resources__.
| class | td-max-width-on-larger-screens | Additional HTML class for the `<div>` containing the box with the attachments. The default value ensures that the box is the same width as other typical content.
| num_prec | 1 | Parameter for formating file size: Number of decimal places
| num_fmt | - , .| Parameter for formating file size (see [Hugo docs](https://gohugo.io/functions/numfmt/)).
| num_fmt_del | " " (=blank) | Corresponding delimiter for parameter for formating file size (see [Hugo docs](https://gohugo.io/functions/numfmt/)).
| empty_list |  No attachments found. | Shown message if file list is empty.
| show_folder | false | Option to show also the relative file path, when paramter `folder` is used.


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

Especially for __none page bundles__ (not `index.md` or `_index.md`) it is also possible to set a specific subfolder for attachments::  
```md
{{</* attachments folder="files" title="Files in folder" /*/>}}
```

{{< attachments folder="files" title="Files in folder" />}}

## Using filter options

The resulting file list can be filtered by the options `filter` (by using [RegEx](https://gohugo.io/functions/findre/ "Docs from used Hugo function for RegEx filtering.") on the filename relative to the current page). 

```md
{{</* attachments title="Filtered page resources for jpg files" filter=".+\.(?i)(jpg|jpeg)$" /*/>}}
```

{{< attachments title="Filtered page resources for jpg files" filter=".+\.(?i)(jpg|jpeg)$" />}}

```md
{{</* attachments folder="./" title="Filtered all files in base folder for 'doc'" filter="doc" */>}}
Also the file `document.pdf` get listed, because it begins with "doc".
{{</* /attachments */>}}
```

{{< attachments folder="./" title="Filtered all files in base folder for 'doc'" filter="doc" >}}
Also the file `document.pdf` get listed, because it begins with "doc".
{{< /attachments >}}

If displaying page resources alternatively the parameter `match` can get used as file list filter. __But [Glob pattern](https://gohugo.io/content-management/page-resources/#pattern-matching "Link to pattern examples") has to be used and the name of the page resource instead of the file name get filtered!__

```md
{{</* attachments title="Filtered page resources for 'files/*'" match="files/*" /*/>}}
```

{{< attachments title="Filtered page resources for 'files/*'" match="files/*" />}}

## All files in this test content
```md
{{</* attachments folder="./" title="All files" exclude="." show_folder=true /*/>}}
```

{{< attachments folder="./" title="All files" exclude="." show_folder=true />}}
