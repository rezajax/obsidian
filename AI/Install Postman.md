**Extract the Archive**:

- **Extract the Archive**:
    
    - Open the terminal and navigate to your `Downloads` folder:
        
        bash
        
        Copy code
        
        `cd ~/Downloads`
        
    - Extract the file into `/opt/`:
        
        bash
        
        Copy code
        
        `sudo tar -xvf postman.tar.gz -C /opt/`
        
- **Create a Symbolic Link** (Optional but recommended):
    
    - To make Postman accessible from anywhere, create a symbolic link in `/usr/local/bin`:
        
        bash
        
        Copy code
        
        `sudo ln -s /opt/Postman/Postman /usr/local/bin/postman`
        
- **Create a Desktop Shortcut** (Optional for GUI access):
    
    - Create a `.desktop` file for Postman:
        
        bash
        
        Copy code
        
        `sudo nano /usr/share/applications/postman.desktop`
        
    - Add the following content:
        
        ini
        
        Copy code
        
        `[Desktop Entry] Name=Postman Exec=/opt/Postman/Postman Icon=/opt/Postman/app/resources/app/assets/icon.png Type=Application Categories=Development;Utility;`
        
    - Save the file (`Ctrl + O`, then `Ctrl + X`).
### **Use `update-desktop-database` Command**

- If the `.desktop` file was placed in `/usr/share/applications/` or `~/.local/share/applications/`, you can manually update the desktop database by running:
    
    bash
    
    Copy code
    
    `sudo update-desktop-database`
### **Refresh the Desktop Environment with `xdg-desktop-menu`**

- If the previous step doesn’t work, you can also try refreshing with `xdg-desktop-menu`:
    
    bash
    
    Copy code
    
    `xdg-desktop-menu forceupdate`