<%*
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

listFolderTree(rootFolder);

%>


