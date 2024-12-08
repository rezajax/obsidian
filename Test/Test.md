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


\```dataviewjs // PS. remove backslash \ at the very beginning! dv.span("** 😊 Title 😥**") /* optional ⏹️💤⚡⚠🧩↑↓⏳📔💾📁📝🔄📝🔀⌨️🕸️📅🔍✨ */ const calendarData = { year: 2022, // (optional) defaults to current year colors: { // (optional) defaults to green blue: ["#8cb9ff", "#69a3ff", "#428bff", "#1872ff", "#0058e2"], // first entry is considered default if supplied green: ["#c6e48b", "#7bc96f", "#49af5d", "#2e8840", "#196127"], red: ["#ff9e82", "#ff7b55", "#ff4d1a", "#e73400", "#bd2a00"], orange: ["#ffa244", "#fd7f00", "#dd6f00", "#bf6000", "#9b4e00"], pink: ["#ff96cb", "#ff70b8", "#ff3a9d", "#ee0077", "#c30062"], orangeToRed: ["#ffdf04", "#ffbe04", "#ff9a03", "#ff6d02", "#ff2c01"] }, showCurrentDayBorder: true, // (optional) defaults to true defaultEntryIntensity: 4, // (optional) defaults to 4 intensityScaleStart: 10, // (optional) defaults to lowest value passed to entries.intensity intensityScaleEnd: 100, // (optional) defaults to highest value passed to entries.intensity entries: [], // (required) populated in the DataviewJS loop below } //DataviewJS loop for (let page of dv.pages('"daily notes"').where(p => p.exercise)) { //dv.span("<br>" + page.file.name) // uncomment for troubleshooting calendarData.entries.push({ date: page.file.name, // (required) Format YYYY-MM-DD intensity: page.exercise, // (required) the data you want to track, will map color intensities automatically content: "🏋️", // (optional) Add text to the date cell color: "orange", // (optional) Reference from *calendarData.colors*. If no color is supplied; colors[0] is used }) } renderHeatmapCalendar(this.container, calendarData) ```