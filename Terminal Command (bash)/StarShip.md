
Install nerdFonts
```bash
sudo mkdir -p /usr/share/fonts/JetBrainsMono
sudo mv ~/Downloads/font/*.ttf /usr/share/fonts/JetBrainsMono/
#sudo mv ~/Downloads/font/*.otf /usr/share/fonts/JetBrainsMono/
sudo fc-cache -f -v
```

### 1. JetBrains Nerd Font

- **Proportional** (عرض متغیر برای کاراکترها).
- دارای **Ligatures** (اتصال خودکار برخی کاراکترها مثل => و != ).
- مناسب برای مطالعه متن و طراحی UI، اما برای کدنویسی ایده‌آل نیست.
- - برخی حروف پهن‌تر از بقیه هستند، که خوانایی متون عادی را بهتر می‌کند.

### 2. JetBrains Nerd Font Mono

- **Monospaced** (همه کاراکترها عرض یکسان دارند).
- دارای **Ligatures** برای نمادهای برنامه‌نویسی.
- مناسب برای **IDE، ترمینال، و محیط‌های کدنویسی**.

### 3. JetBrainsNL Nerd Font

- **Proportional** مثل نسخه اصلی، اما بدون **Ligatures**.
- مناسب برای محیط‌هایی که نیاز به فونت Proportional دارند ولی Ligatures را نمی‌خواهند.

### 4. JetBrainsNL Nerd Font Mono

- **Monospaced** بدون **Ligatures**.
- مناسب برای **ترمینال، IDE، و محیط‌های کدنویسی که Ligatures را پشتیبانی نمی‌کنند یا نمی‌خواهید استفاده کنید**.



# Install zsh and ohmyzsh
اگر **Oh My Zsh** را نصب کرده باشید، **Starship** فقط جایگزین نمایش پرامپت (`PS1`) می‌شود، اما قابلیت‌های Zsh مثل آلیاس‌ها و افزونه‌ها همچنان کار می‌کنند.

```bash
sudo apt inatall zsh

sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"


```
# Install StarShip
```bash
curl -sS https://starship.rs/install.sh | sh

# if bash
echo 'eval "$(starship init bash)"' >> ~/.bashrc
source ~/.bashrc

# if zsh
echo 'eval "$(starship init zsh)"' >> ~/.zshrc
source ~/.zshrc


$ vi ~/.zshrc
plugins=(
  git
  gradle
  sdk
  zsh-autosuggestions
  zsh-syntax-highlighting
  fzf
  z
  autojump
  aliases
  command-not-found
)

# install custom plugin
# rez: i don't use package manager ohmyzsh "antigen" for install zsh-autosuggestions, zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
sudo apt install fzf
sudo apt install autojump


source ~/.zshrc

```


---

مشکل پیشنهاد نصب برنامه 
```bash
# add to ~/.zshrc
`[[ -f /etc/zsh_command_not_found ]] && source /etc/zsh_command_not_found`
# or add plugin ~/.zshrc
`plugins=(command-not-found)
```


tstSocks on  master [!] via 🅶 v8.9 via ☕ v21.0.6 via 🅺 ❯ nvim zsh: command not found: nvim tstSocks on  master [!] via 🅶 v8.9 via ☕ v21.0.6 via 🅺 ❯ bash tstSocks on  master [!] via 🅶 v8.9 via ☕ v21.0.6 via 🅺 ❯ nvim Command 'nvim' not found, but can be installed with: sudo apt install neovim tstSocks on  master [!] via 🅶 v8.9 via ☕ v21.0.6 via 🅺 ❯ چرا توی bash پیشنهاد میده nvim رو ندارم برم نصب کنم ولی تو ohmyzsh نشون نمیده!

###### ChatGPT said:

چون `oh-my-zsh` معمولاً قابلیت **"command correction"** رو داره، اما ممکنه این قابلیت در تنظیمات غیرفعال شده باشه یا `oh-my-zsh` خطاهای `command not found` رو خودش مدیریت کنه و پیشنهاد نصب رو نمایش نده.

### بررسی علت و حل مشکل:

1. **بررسی فعال بودن command-not-found در Zsh:**  
    توی `bash`، پکیج `command-not-found` به صورت پیش‌فرض فعاله و وقتی یه دستوری که نصب نیست رو اجرا می‌کنی، پیشنهاد نصبش رو میده. اما در `zsh` ممکنه این قابلیت غیرفعال باشه. برای فعال کردنش این دستور رو بزن:
    
    sh
    
    CopyEdit
    
    `source /etc/zsh_command_not_found`
    
    اگر جواب داد، این خط رو به `~/.zshrc` اضافه کن:
    
    sh
    
    CopyEdit
    
    `[[ -f /etc/zsh_command_not_found ]] && source /etc/zsh_command_not_found`
    
    بعد `zsh` رو ریلود کن:
    
    sh
    
    CopyEdit
    
    `exec zsh`
    
2. **بررسی `command_not_found_handle` در Bash و Zsh:**  
    بزن ببین تو `bash` چی تنظیم شده:
    
    sh
    
    CopyEdit
    
    `type command_not_found_handle`
    
    و تو `zsh` هم:
    
    sh
    
    CopyEdit
    
    `type command_not_found_handle`
    
    احتمالاً تو `bash` یه اسکریپت برای پیشنهاد نصب داره، اما تو `zsh` این تابع تنظیم نشده.
    
3. **بررسی پلاگین‌های `oh-my-zsh`:**  
    ممکنه پلاگینی که این قابلیت رو تو `zsh` اضافه می‌کنه فعال نباشه. چک کن که `zsh-command-not-found` نصب شده و توی `.zshrc` این خط باشه:
    
    sh
    
    CopyEdit
    
    `plugins=(command-not-found)`
    
    اگر نبود، اضافه کن و `zsh` رو ریلود کن.
    

### نتیجه:

**توی `bash`، Ubuntu/Debian به صورت پیش‌فرض پکیج `command-not-found` رو داره، ولی تو `zsh` باید به صورت دستی فعالش کنی.**  
اگر `oh-my-zsh` داری، بهتره `command-not-found` رو توی پلاگین‌هاش فعال کنی.


