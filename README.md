
<p align="center">
  <img alt="Ironchip icon" src="/assets/icon.png" width="100"/>
</p>

<h1 align="center">Ironchip macOS</h1>

<p align="center">
  <img alt="macOS badge" src="https://img.shields.io/badge/macOS-D3D3D3?logo=apple&logoColor=black"/>
  <img alt="Latest version" src="https://img.shields.io/github/v/release/Ironchip-Security/Ironchip-Mac-Logon?color=green"/>
</p>

## IDENTITY PROTECTION

Elevate your cybersecurity strategy with Ironchip Identity Platform, designed to bring the power of Multi-Factor Authentication (MFA) to your desktop computing environment. [Know more](https://www.ironchip.com/en/mobileless-authentication).

**Role-based privilege management:**  
Set different user privileges to prevent unauthorized users from misusing the system.

**Restrict access from unauthorized places:**  
Limit access to authorized areas for enhanced security.

**Supervision of accesses in real time:**  
Monitor user activity, view access history, generate reports, and download them for complete control.

**Intrusion detection system (IDS):**  
Receive alerts for SIM swapping, phishing, device switching, and more.

<p align="center">
 <a href="https://www.youtube.com/watch?v=G-rr6BzcQZ0"> 
  <img alt="Logon showcase gif" src="./assets/showcase-logon.gif" width="550"/>
 </a>
</p>

---

## Ironchip PAM for macOS

### What it is

This PAM module integrates Ironchip Multi-Factor Authentication (MFA) into the macOS login flow, administrator actions (`sudo`), SSH sessions, and more.

---

### Download

Download the latest Ironchip PAM module for macOS (`.so` file):

<p align="left">
  <a href="https://github.com/Ironchip-Security/Ironchip-Mac-Logon/releases/latest/download/pam_ironchip_auth.so">
    <img alt="Download Ironchip Module" src="https://custom-icon-badges.demolab.com/badge/-Download%20Module-blue?style=for-the-badge&logo=download&logoColor=white">
  </a>
</p>

---

### Basic Usage

Once you've downloaded the `.so` file:

1. Move it to a secure directory:
   ```bash
   sudo mv pam_ironchip_auth.so /usr/local/lib/security/
   ```

2. Edit your desired PAM configuration file (e.g., `/etc/pam.d/sudo`) and add:
   ```bash
   auth required /usr/local/lib/security/pam_ironchip_auth.so host=https://api.ironchip.com api_key=<your_api_key>
   ```

3. Save and close the file (`Ctrl+O`, `Enter`, `Ctrl+X` if using `nano`).

4. Assign access from the [Ironchip Dashboard](https://app.ironchip.com).

---

## Installation & Configuration

> **Important:** This process can cause permanent system and user locks if not executed correctly. Keep a terminal with administrator permissions open during the process to avoid any irreparable error. It is recommended to first test the integration with `sudo` authentication to avoid being locked out of the system.

### Step 1: Prepare the PAM directory

If it doesn't exist, create the directory:

```bash
sudo mkdir -p /opt/local/lib/pam
```

### Step 2: Copy the PAM module

Download the PAM file provided by Ironchip and copy it to the directory:

```bash
sudo cp <path_to_pam_file> /opt/local/lib/pam/
```

Replace `<path_to_pam_file>` with the actual path to your `.so` file.

---

### Step 3: Update PAM configuration

Edit one of the following files under `/etc/pam.d/` depending on where you want Ironchip authentication:

- `sudo` — Authenticate on administrative actions (`sudo`, `sudo su`)
- `authorization` or `screensaver` — Authenticate on macOS login
- `sshd` — Authenticate on remote SSH login

**Example: Add MFA to sudo**

```bash
sudo nano /etc/pam.d/sudo
```

Add the following line at the **top** of the file:

```bash
auth required /opt/local/lib/pam/pam_ironchip_auth.so host=https://api.ironchip.com api_key=<your_api_key>
```

Replace `<your_api_key>` with the actual key from your Ironchip application.

Save and exit: `Ctrl+O`, `Enter`, then `Ctrl+X`.

---

### Step 4: Remove macOS quarantine attribute

Disable macOS's protection for unidentified developers on the PAM file:

```bash
xattr -dr com.apple.quarantine /opt/local/lib/pam/pam_ironchip_auth.so
```

---

### Uninstall / Revert

To revert the integration:

1. Remove the added line from the modified `/etc/pam.d/` file.
2. Delete the PAM module:

```bash
sudo rm /opt/local/lib/pam/pam_ironchip_auth.so
```

---

### 📘 Documentation

For more information and advanced options, visit the <a href="https://docs.ironchip.com/en/mac-logon" target="_blank" rel="noopener noreferrer">Ironchip macOS documentation</a>.
