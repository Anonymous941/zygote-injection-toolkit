# Zygote injection toolkit
This is a Python command-line utility to easily run and backup private app data using the Android Zygote injection vulnerability (CVE-2024-31317).
To run this, you must have any device that has _not_ been updated to the [June 1, 2024 security patch](https://source.android.com/security/bulletin/2024-06-01).  If you don't know whether your device is vulnerable or not, simply run the script and it will check for you.

To run it, you need to have ADB installed and USB debugging enabled.
### Installation
To install or update, simply run `pip install --upgrade git+https://github.com/Anonymous941/zygote-injection-toolkit`.

If you would like to make changes to the source code, instead clone the repository using `git clone` and run `pip install -e .`.  This will install it in [development mode](https://setuptools.pypa.io/en/latest/userguide/development_mode.html).
### Usage
Make sure USB debugging is enabled and ADB is running (this can be done by running `adb start-server`, or almost any other ADB command).  Then simply run `python -m zygote_injection_toolkit`.  If the exploit runs successfully, you should have a reverse shell on port 1234 (on your host and the Android device), running with `system` priviledges.  It will also automatically attempt to force-enable OEM unlocking.
### About the exploit
**This is not a root exploit!**  It is not possible to run apps requiring root, or install any Magisk modules.  If you are already rooted, then you do not need to run this exploit.

What it can do is execute arbitrary code as the `system` user.  It has the ability to impersonate any app, including privileged apps, and read/write their private data (including data that cannot be backed up using `adb backup`).

Here are some use cases:

- Backing up almost all data before unlocking the bootloader, which wipes everything for security purposes
- Messing with system apps' data in order to bypass OEM restrictions
- This automatically tries to bypass carrier restrictions on bootloader unlocking, which *might* allow you to unlock the bootloader, but this is unlikely to be the only protection
- Chaining with a root exploit (outside the scope of this repository)

For more information about the exploit itself, you can refer to these two writeups: https://rtx.meta.security/exploitation/2024/06/03/Android-Zygote-injection.html, https://infosecwriteups.com/exploiting-android-zygote-injection-cve-2024-31317-d83f69265088
