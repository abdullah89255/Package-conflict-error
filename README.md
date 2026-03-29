# Package-conflict-error
You’re hitting a **package conflict error** in `dpkg` — this happens when two packages try to install the **same file**.

### ❌ Problem

* `pyinstaller-hooks-contrib (2025.11-1)`
  is trying to overwrite a file that already exists in:
* `python3-pyinstaller-hooks-contrib (2025.1-0kali1)`

So `dpkg` refuses to continue.

---

## ✅ Fix (Safe & Recommended)

### 🔧 Step 1: Fix broken packages

Run:

```bash
sudo apt --fix-broken install
```

---

### 🔧 Step 2: Remove the conflicting old package

```bash
sudo apt remove python3-pyinstaller-hooks-contrib -y
```

---

### 🔧 Step 3: Reinstall properly

```bash
sudo apt install pyinstaller-hooks-contrib -y
```

---

## ⚡ Alternative (Force overwrite – use carefully)

If you want a quick fix:

```bash
sudo dpkg -i --force-overwrite /var/cache/apt/archives/pyinstaller-hooks-contrib_2025.11-1_all.deb
sudo apt --fix-broken install
```

⚠️ This forces installation, but may cause future dependency issues.

---

## 🧠 Why this happens

* Kali (or Debian-based systems) sometimes split packages differently
* You already had `python3-pyinstaller-hooks-contrib`
* Now installing a newer `pyinstaller-hooks-contrib` → file conflict

---

## 🧹 Optional cleanup

After fixing:

```bash
sudo apt clean
sudo apt autoremove
```

---

## 🚀 Pro Tip

470 packages “not fully installed” is a red flag. After fixing this, run:

```bash
sudo dpkg --configure -a
sudo apt update && sudo apt upgrade
```

---


