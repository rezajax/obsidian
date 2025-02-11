
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
)

# install custom plugin
# rez: i don't use package manager ohmyzsh "antigen" for install zsh-autosuggestions, zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
sudo apt install fzf
sudo apt install autojump


source ~/.zshrc

```