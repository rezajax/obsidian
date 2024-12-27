---
title: Welcome to Quartz
---
[English Folder](/English)
[Test Folder](/Test)
[Redis Folder](/Redis)
[AI folder](/AI)


This is First Reza run. Sepi is here.

<% tp.date.now() %>



# Directory Listing for `<% tp.file.cursor() %>`

<%*
const { readdirSync, statSync } = app.plugins.plugins["templater"].app.vault.adapter;
const folderPath = tp.file.folder(true); // Get the current folder path
const indent = (level) => "  ".repeat(level); // Create indentation for nested items

function listFiles(dirPath, level = 0) {
    let output = "";
    const items = readdirSync(dirPath).sort(); // Get and sort files/folders
    for (const item of items) {
        const fullPath = `${dirPath}/${item}`;
        const isFolder = statSync(fullPath).isDirectory();
        if (isFolder) {
            output += `${indent(level)}- **${item}/**\n`; // Bold folders
            output += listFiles(fullPath, level + 1); // Recursively list subfolders
        } else {
            output += `${indent(level)}- [${item}](./${item})\n`; // Link to files
        }
    }
    return output;
}

tR += listFiles(folderPath); // Generate and insert directory tree
%>



Callouts List
https://obsidian.rocks/using-callouts-in-obsidian/

note (blue)
abstract, summary, tldr (green)
info (blue)
todo (blue)
tip, hint, important (sky blue)
success, check, done (green)
question, help, faq (yellow)
warning, caution, attention (orange)
failure, fail, missing (red)
danger, error (red)
bug (red)
example (purple)
quote, cite (grey)

> [!abstract] Quote
> cite


> [!bug] Title
> Contents , Just for test

> [!TIP] Title
> Contents

> [!Warning] Title
> Contents

> [!Info] Title
> Contents


This is reza


23

new line with git module

public 1



# Project Tree

```dataviewjs
// Set root folder for the tree; empty string means entire vault
const rootFolder = "";

// Helper function to create a nested tree
function listFolderTree(folderPath, indent = "") {
    // Retrieve all pages and folders in the given path
    const items = dv.pages(`"${folderPath}"`)
        .file
        .sort(p => p.path, "asc");

    for (const item of items) {
        const relativePath = item.path.replace(rootFolder, "").trim();
        const isFolder = item.folder && relativePath.endsWith("/");

        if (isFolder) {
            // Display the folder name in bold
            dv.paragraph(`${indent}- **${relativePath.split("/").pop()}/**`);
            // Recursively list subfolders and files
            listFolderTree(item.path, indent + "  ");
        } else {
            // Display files as clickable links
            dv.paragraph(`${indent}- [${item.name}](${item.path})`);
        }
    }
}

// Generate the tree starting from the root folder
listFolderTree(rootFolder);


```



```dataviewjs
const { readdirSync, statSync } = app.plugins.plugins["templater"].app.vault.adapter;
const rootFolder = ""; // Root folder for the tree; leave empty for the entire vault

// Helper function to list the folder tree
function listFolderTree(dirPath, indent = "") {
    let output = "";
    const items = readdirSync(dirPath).sort(); // Sort items alphabetically
    for (const item of items) {
        const fullPath = `${dirPath}/${item}`;
        const isFolder = statSync(fullPath).isDirectory();
        if (isFolder) {
            output += `${indent}- **${item}/**\n`;
            output += listFolderTree(fullPath, indent + "  "); // Recursively list subfolders
        } else {
            output += `${indent}- [${item}](${fullPath})\n`;
        }
    }
    return output;
}

tR += `# Project Tree\n\n`;
tR += listFolderTree(rootFolder);
```

