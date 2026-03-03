
# Kernel Management Script for RHEL
This project includes a script that automates the checking of the version of the running kernel by comparing it with the latest installed kernel version for a system running Red Hat Enterprise Linux (RHEL), ensuring the system is running the latest kernel version, and prompting the user for an update if a newer version of the kernel exists.

## Features
- It checks the kernels that are currently installed and the kernel that is currently booted.
- It compares the kernel that is currently booted with the latest kernel that is installed.
- It prompts the user if a new kernel is available, allowing the user to choose whether to install and boot into the latest kernel.
- It does not make any changes if the current kernel is the latest kernel.

## Prerequisites
- Red Hat Enterprise Linux 7.x or later versions.
- Ensure you have `yum` package manager installed and working.
- Root or sudo access is required for installation and rebooting the system.

## How it works
- Check Installed Kernels: This function lists all the installed kernels using the rpm -qa | grep -i kernel command.
- Check Current Booted Kernel: This function shows the currently booted kernel using the uname -r command.
- Compare with the Latest Kernel: The script compares the currently booted kernel with the latest kernel using the rpm -q --last kernel command.
- Prompt the User: The script prompts the user to install and reboot into the latest kernel if it is not currently booted.
  - If the currently booted kernel is the same as the latest kernel, it simply exits the script.
- Latest Kernel Check: The script checks if the currently booted kernel is the latest kernel and exits the script if it is.

## How to Use
1. **Make the Script Executable**:
   After downloading script, ensure that the script has execution permissions:
   ```bash
   chmod +x kernelcheck.sh

3. **Run the Script**:
   Execute the script using `sudo` to check your system’s kernel status:
   ```bash
   sudo ./kernelcheck.sh
   ```

The script will:
   - List all the installed kernels.
   - Verify the running kernel.
   - If a new kernel is present but not running, it will prompt to install and reboot to the new kernel.

4. **Example Output**:
   ```bash
   Checking installed kernels...
   kernel-tools-3.10.0-1160.119.1.el7.x86_64
   kernel-3.10.0-1160.119.1.el7.x86_64
   kernel-3.10.0-1160.el7.x86_64
   kernel-3.10.0-1160.83.1.el7.x86_64
   abrt-addon-kerneloops-2.1.11-60.el7.x86_64
   kernel-tools-libs-3.10.0-1160.119.1.el7.x86_64
   Currently booted kernel: 3.10.0-1160.119.1.el7.x86_64
   The system is already running the latest kernel: 3.10.0-1160.119.1.el7.x86_64
   ```
5. **Testing with an Older Kernel**:
   To test the system under a condition where the latest kernel version is not being used, the following steps have to be taken:
   - Boot the system and, upon the GRUB screen, manually select the older kernel version.
   - Run the script again to test the functionality of the script when the latest kernel version is available but not being utilized by the system.

## FAQ
### What happens if I choose not to install the latest kernel?
The script will exit without making any changes to your system, leaving the currently booted kernel the way it was.

### How do I go back to the latest kernel after testing?
If you have booted into an older kernel for testing, you can simply reboot and boot the latest kernel by selecting it from the GRUB menu, or you can have the script install and reboot into the latest kernel if you answer the prompt correctly.

## Contributing
Feel free to open issues or submit pull requests to improve the script or add more features.

## License
MIT License

