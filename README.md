# Ubuntu Auto Install Configuration

## Overview
This project contains an **autoinstall.yaml** file designed for automating the installation of Ubuntu with pre-configured settings. It utilizes **cloud-init** to streamline the installation process, setting up user credentials, system locale, keyboard layout, timezone, essential packages, and more.

## Features
- **Automated Installation**: No manual intervention required.
- **User & System Setup**: Configures a predefined user, hostname, and password.
- **Localization**: Sets up Brazilian Portuguese as the default locale and keyboard layout.
- **Pre-installed Software**:
  - **APT Packages**: LibreOffice, GIMP, Git, Wget.
  - **Snap Packages**: Spotify (Stable Channel).
- **Multimedia Codecs**: Ensures proper playback support.
- **Drivers Installation**: Automatically installs necessary drivers.
- **System Updates**: Enables automatic updates.
- **Auto Reboot**: System reboots after the installation is completed.

## Configuration Details
The following parameters are pre-configured in `autoinstall.yaml`:

```yaml
#cloud-config
autoinstall:
    version: 1
    identity:
        realname: 'Dionatan Simioni'
        hostname: ubuntu-desktop
        username: diolinux
        password: '<ENCRYPTED_PASSWORD>'
    locale: pt_BR.utf8
    keyboard:
        layout: br
    timezone: "America/Sao_Paulo"
    packages:
        - libreoffice
        - gimp
        - git
        - wget
    snaps:
        - name: spotify
          channel: stable
          classic: false
    codecs:
        install: true
    drivers:
        install: true
    updates: all
    shutdown: reboot
```

## Usage Instructions
### 1. Preparing the Installation Media
1. Download the latest Ubuntu ISO.
2. Create a bootable USB using **Rufus**, **balenaEtcher**, or **Ventoy**.
3. Place `autoinstall.yaml` in the root of the USB under the `cidata` folder.

### 2. Booting and Installation
1. Boot the target machine from the USB drive.
2. Ubuntu will automatically detect `autoinstall.yaml` and proceed with the installation.
3. Once the installation is complete, the system will reboot automatically.

## Generating an Encrypted Password
To generate an encrypted password for use in `autoinstall.yaml`, use the following command:

```bash
sudo apt update && sudo apt install whois -y
mkpasswd --method=yescrypt "your_password_here"
```

Replace `"your_password_here"` with your desired password. The generated encrypted password can be used in the `password` field of the YAML file.

## Security Considerations
- The password is stored in an encrypted format using **bcrypt**.
- Ensure `autoinstall.yaml` is stored securely and removed after installation.

## Customization
To modify the installation settings, edit `autoinstall.yaml` before use:
- **Change username and password** under `identity`.
- **Modify software packages** by adding or removing entries under `packages` and `snaps`.
- **Adjust locale and timezone** as needed.

## License
This project is licensed under the MIT License. Feel free to modify and distribute it.

## Author
**Dionatan Simioni**
- GitHub: [@diolinux](https://github.com/diolinux)
- Website: [diolinux.com.br](https://www.diolinux.com.br)

---
**Enjoy a seamless Ubuntu installation with this pre-configured setup!** 🚀
