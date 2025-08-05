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
Set different user privileges. Prevents unauthorized users from accessing the rest of the system and misusing information, mitigating malicious users.

**Restrict access from unauthorized places:**  
Generate enabled access from authorized areas and take your security to the next level.

**Supervision of accesses in real time:**  
Check user activity, view access on a timeline, get reports and download them for full control.

**Intrusion detection system (IDS):**  
Location-based reporting system to alert of sim swapping, phishing, device switching, etc.

<p align="center">
 <a href="https://www.youtube.com/watch?v=G-rr6BzcQZ0"> 
  <img alt="Logon showcase gif" src="./assets/showcase-logon.gif" alt="animated" width="550"/>
 </a>
</p>

## Logon

### What it is  
Logon is a custom Windows credential provider by [Ironchip](https://www.ironchip.com/) that integrates Multi-Factor Authentication (MFA) directly into the Windows login experience.

**Cached Passwords:**  
Our simplified access can enhance user experience, making it more convenient and user-friendly. This is especially valuable in a work or personal environment where you're required to log in to various systems multiple times a day.

**Extra Layer:**  
MFA adds an extra layer of protection, requiring multiple forms of authentication, such as a password and a one-time code or push notification. 

**Improved Compliance:**  
MFA helps organizations meet compliance requirements and security standards by implementing robust authentication methods.

### Download the latest Ironchip PAM module for macOS (`.so` file):

<p align="left">
  <a href="https://github.com/Ironchip-Security/Ironchip-Mac-Logon/releases/latest/download/pam_ironchip_auth_all.so">
    <img alt="Download Ironchip Module" src="https://custom-icon-badges.demolab.com/badge/-Download%20Module-blue?style=for-the-badge&logo=download&logoColor=white">
  </a>
</p>

### Manual Installation (via Terminal)

This module integrates Ironchip MFA into macOS login using PAM.

#### Step 1: Copy the module to the PAM directory  
```bash
sudo mkdir -p /usr/local/lib/security/
sudo cp pam_ironchip_auth_all.so /usr/local/lib/security/
```

#### Step 2: Update PAM configuration  
Open the PAM login config file:
```bash
sudo nano /etc/pam.d/login
```

Add this line near the top of the file:
```bash
auth required /usr/local/lib/security/pam_ironchip_auth_all.so
```

Save and exit (Ctrl+O, Enter, Ctrl+X).

#### Step 3: Test the configuration  
Lock your Mac or logout and try logging in to verify that Ironchip MFA is active.

---

If you want to uninstall or revert changes, remove the added line from `/etc/pam.d/login` and delete the `.so` file from `/usr/local/lib/security/`.

---

For more information and advanced options, visit the <a href="https://docs.ironchip.com/en/mac-logon" target="_blank" rel="noopener noreferrer">Ironchip macOS documentation</a>.
