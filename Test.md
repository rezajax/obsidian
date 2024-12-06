---
tags:
  - hi
---

hi

```dataview
table file.link as File
from ""
where contains(text, "hi")

```


تمام فایل هایی که شامل کلمه hi هستند

```dataviewjs
const searchTerm = "hi"; // کلمه‌ای که می‌خواهید جستجو کنید

// تمام فایل‌های Markdown را می‌گیریم
const files = app.vault.getMarkdownFiles();

// لیست فایل‌هایی که شامل searchTerm هستند
const results = [];

for (const file of files) {
    const content = await app.vault.read(file); // خواندن محتوای فایل
    if (content.includes(searchTerm)) {
        results.push(file);
    }
}

// نمایش فایل‌هایی که کلمه را شامل می‌شوند
dv.table(["File"], results.map(f => [f.basename]));

```

```temp

// Get all folders
<%
tp.app.vault.getAllLoadedFiles()
  .filter(x => x instanceof tp.obsidian.TFolder)
  .map(x => x.name)
%>

// Update frontmatter of existing file
<%*
const file = tp.file.find_tfile("path/to/file");
await tp.app.fileManager.processFrontMatter(file, (frontmatter) => {
  frontmatter["key"] = "value";
});
%>
```