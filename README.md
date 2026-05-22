
---

## 📋 جدول المحتويات

- [لقطات الشاشة](#-لقطات-الشاشة)
- [متطلبات النظام](#-متطلبات-النظام)
- [أولى الخطوات بعد التثبيت](#-أولى-الخطوات-بعد-التثبيت)
- [AUR Helper](#-aur-helper--yay)
- [الدرايفرات](#-الدرايفرات)
- [الثيم — Dracula](#-الثيم--dracula)
- [الألعاب](#-الألعاب)
- [الدراسة والتطوير](#-الدراسة-والتطوير)
- [التصفح](#-التصفح)
- [Pamac — مدير الحزم](#-pamac--مدير-الحزم)
- [تحسينات الأداء](#-تحسينات-الأداء)
- [البرامج المثبتة](#-البرامج-المثبتة)
- [النسخ الاحتياطي](#-النسخ-الاحتياطي)

---

## 🖼 لقطات الشاشة
![[Screenshots/Screenshot_2026-05-22_20-20-48.png]]
![[Screenshots/Screenshot_2026-05-22_20-18-38.png]]
![[Screenshots/Screenshot_2026-05-22_20-20-08.png]]

```
screenshots/
├── desktop.png
├── terminal.png
├── gaming.png
└── workflow.png
```

---

## 💻 متطلبات النظام

| المكوّن | الحد الأدنى | الموصى به |
|---|---|---|
| المعالج | x86_64 Dual-Core | Quad-Core+ |
| الذاكرة | 2 GB RAM | 8 GB+ |
| التخزين | 20 GB | 50 GB+ SSD |
| الاتصال | مطلوب للتثبيت | — |

---

## 🚀 أولى الخطوات بعد التثبيت

```bash
# 1. تحديث النظام كاملاً
sudo pacman -Syu

# 2. تفعيل multilib (للألعاب و32-bit)
sudo nano /etc/pacman.conf
# أزل التعليق عن:
# [multilib]
# Include = /etc/pacman.d/mirrorlist

sudo pacman -Syu

# 3. تثبيت الأدوات الأساسية
sudo pacman -S base-devel git wget curl
```

---

## 📦 AUR Helper — yay

```bash
git clone https://aur.archlinux.org/yay.git
cd yay && makepkg -si
cd .. && rm -rf yay
```

**الأوامر الأساسية:**

```bash
yay -S  <حزمة>     # تثبيت
yay -R  <حزمة>     # إزالة
yay -Syu            # تحديث الكل (pacman + AUR)
yay -Ss <كلمة>     # بحث
```

---

## 🔧 الدرايفرات

### الصوت — PipeWire

```bash
sudo pacman -S pipewire pipewire-alsa pipewire-pulse wireplumber
systemctl --user enable --now pipewire pipewire-pulse wireplumber
```

### الفيديو

```bash
# ── AMD ──────────────────────────────────────────────
sudo pacman -S mesa vulkan-radeon lib32-mesa lib32-vulkan-radeon

# ── NVIDIA ───────────────────────────────────────────
sudo pacman -S nvidia nvidia-utils lib32-nvidia-utils

# ── Intel ─────────────────────────────────────────────
sudo pacman -S mesa vulkan-intel lib32-mesa lib32-vulkan-intel
```

---

## 🧛 الثيم — Dracula

### GTK Theme

```bash
yay -S dracula-gtk-theme dracula-icons-git
```

### تطبيق الثيم في XFCE

```
Settings → Appearance → Style   → Dracula
Settings → Appearance → Icons   → Dracula
Settings → Window Manager → Style → Dracula
```

### Terminal (Xfce4-Terminal)

```bash
mkdir -p ~/.config/xfce4/terminal/colorschemes
wget -O ~/.config/xfce4/terminal/colorschemes/Dracula.theme \
  https://raw.githubusercontent.com/dracula/xfce4-terminal/master/Dracula.theme
```

ثم: `Terminal → Preferences → Colors → Load Preset → Dracula`

### GTK4

```bash
mkdir -p ~/.config/gtk-4.0
ln -sf ~/.themes/Dracula/gtk-4.0/gtk.css ~/.config/gtk-4.0/gtk.css
ln -sf ~/.themes/Dracula/gtk-4.0/gtk-dark.css ~/.config/gtk-4.0/gtk-dark.css
```

### VS Code

```
Ctrl+Shift+X → "Dracula Official" → Install
Ctrl+K Ctrl+T → Dracula
```

---

## 🎮 الألعاب

### Steam + Proton

```bash
sudo pacman -S steam

# تفعيل Proton للألعاب المدعومة وغير المدعومة:
# Steam → Settings → Compatibility → Enable Steam Play for all titles
```

### Proton-GE (توافق أفضل)

```bash
yay -S proton-ge-custom
# اختره من: Steam → بروبرتيز اللعبة → Compatibility
```

### Lutris (Epic / GOG / Battle.net)

```bash
sudo pacman -S lutris
```

### Wine

```bash
sudo pacman -S wine wine-mono wine-gecko winetricks
```

### تحسين الأداء أثناء اللعب

```bash
# GameMode
sudo pacman -S gamemode lib32-gamemode

# MangoHud (عرض FPS والأداء)
sudo pacman -S mangohud lib32-mangohud
```

**إضافتها في Steam Launch Options:**

```
MANGOHUD=1 gamemoderun %command%
```

---

## 📚 الدراسة والتطوير

### Office

```bash
# LibreOffice (مع دعم عربي)
sudo pacman -S libreoffice-fresh libreoffice-fresh-ar

# WPS Office (أقرب لـ Microsoft)
yay -S wps-office wps-office-mui-ar ttf-wps-fonts
```

### PDF

```bash
sudo pacman -S okular      # قارئ + تعليقات
sudo pacman -S xournalpp   # كتابة على PDF
```

### الملاحظات

```bash
yay -S obsidian            # ملاحظات مترابطة (Markdown)
yay -S joplin-desktop      # مفتوح المصدر مع مزامنة
```

### بيئة التطوير

```bash
# VS Code
yay -S visual-studio-code-bin

# Python
sudo pacman -S python python-pip
pip install jupyter notebook --break-system-packages

# Node.js
sudo pacman -S nodejs npm
```

---

## 🌐 التصفح

```bash
sudo pacman -S firefox       # الافتراضي
yay -S brave-bin             # خصوصية + سرعة
sudo pacman -S chromium      # مفتوح المصدر
```

### إضافات موصى بها

| الإضافة | الغرض |
|---|---|
| uBlock Origin | حجب الإعلانات |
| Bitwarden | مدير كلمات المرور |
| Dark Reader | الوضع المظلم لكل المواقع |

### تحميل الفيديوهات

```bash
sudo pacman -S yt-dlp

yt-dlp "URL"                          # تحميل فيديو
yt-dlp -x --audio-format mp3 "URL"   # صوت فقط
```

---

## 🗂 Pamac — مدير الحزم

```bash
yay -S pamac-aur
```

**تفعيل المصادر:**
```
Pamac → ☰ → Preferences
├── AUR     → Enable ✅
├── Flatpak → Enable ✅
└── Snap    → Enable (اختياري)
```

**Flatpak:**

```bash
sudo pacman -S flatpak
flatpak remote-add --if-not-exists flathub \
  https://flathub.org/repo/flathub.flatpakrepo
```

**أوامر Pamac:**

```bash
pamac search <حزمة>
pamac install <حزمة>
pamac remove <حزمة>
pamac upgrade
pamac clean --build-files
```

---

## ⚡ تحسينات الأداء

### Swappiness

```bash
echo "vm.swappiness=10" | sudo tee /etc/sysctl.d/99-swappiness.conf
sudo sysctl --system
```

### TRIM للـ SSD

```bash
sudo systemctl enable fstrim.timer
```

### Zram

```bash
yay -S zram-generator
```

### Earlyoom (منع التجمد)

```bash
sudo pacman -S earlyoom
sudo systemctl enable --now earlyoom
```

### Preload

```bash
yay -S preload
sudo systemctl enable --now preload
```

---

## 📋 البرامج المثبتة

```bash
sudo pacman -S \
  vlc \               # مشغل وسائط
  flameshot \         # لقطات شاشة
  ark \               # ضغط/فك ضغط
  unrar p7zip \       # فورمات الضغط
  htop \              # مراقب العمليات
  neofetch \          # معلومات النظام
  timeshift           # نسخ احتياطي
```

---

## 💾 النسخ الاحتياطي

```bash
sudo pacman -S timeshift
```

**الإعداد الموصى به:**
```
Timeshift → Settings
├── Snapshot Type  → RSYNC
├── Schedule       → Weekly ✅ + Monthly ✅
└── Keep           → 3 Weekly / 2 Monthly
```

> 📌 خذ snapshot يدوي **فور** الانتهاء من الإعداد وقبل أي تغيير كبير.

---

## 📚 مراجع مهمة

- [Arch Wiki](https://wiki.archlinux.org) — المرجع الأول لأي مشكلة
- [EndeavourOS Forums](https://forum.endeavouros.com)
- [Dracula Theme](https://draculatheme.com)
- [ProtonDB](https://www.protondb.com) — توافق الألعاب مع Linux
