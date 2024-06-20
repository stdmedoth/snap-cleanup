# Snap Cleanup Script

This script is designed to help you manage and clean up old revisions of snaps on your system. It removes all disabled snap revisions to free up space and keep your system tidy.

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [Important Notes](#important-notes)
- [Script Explanation](#script-explanation)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Snap Cleanup Script removes old, disabled revisions of installed snaps. This is particularly useful for maintaining a clean and efficient system, as old revisions can accumulate and consume significant disk space.

## Prerequisites

- **Snapd**: Ensure Snapd is installed on your system. Most modern Linux distributions include Snapd by default. If not, you can install it via your package manager.

- **Bash**: This script is written in Bash. Make sure Bash is available on your system.

## Usage

1. **Clone the Repository or Download the Script**:

   You can clone this repository using Git or simply download the script directly.

   ```bash
   git clone https://github.com/your-username/snap-cleanup-script.git
   cd snap-cleanup-script
   ```

2. **Make the Script Executable**:

   Ensure the script has executable permissions.

   ```bash
   chmod +x snap-cleanup.sh
   ```

3. **Close All Snaps**:

   Before running the script, make sure to close all running snap applications. This is crucial to avoid any potential conflicts or data loss.

4. **Run the Script**:

   Execute the script to remove old, disabled snap revisions.

   ```bash
   ./snap-cleanup.sh
   ```

## Important Notes

- **Backup Important Data**: Always backup important data before running maintenance scripts.
- **Close All Snaps**: As noted, ensure all snaps are closed before running the script.
- **Administrative Privileges**: You may need to run the script with `sudo` if you encounter permission issues.

   ```bash
   sudo ./snap-cleanup.sh
   ```

## Script Explanation

Here's a breakdown of what the script does:

```bash
#!/bin/bash
# Removes old revisions of snaps
# CLOSE ALL SNAPS BEFORE RUNNING THIS
set -eu
LANG=en_US.UTF-8 snap list --all | awk '/disabled/{print $1, $3}' |
    while read snapname revision; do
        snap remove "$snapname" --revision="$revision"
    done
```

- **`#!/bin/bash`**: Specifies the script should be run in the Bash shell.
- **`set -eu`**: 
  - `-e` option tells the script to exit if any command fails.
  - `-u` option causes the script to exit if it tries to use an uninitialized variable.
- **`LANG=en_US.UTF-8`**: Sets the language environment to ensure consistent output format.
- **`snap list --all`**: Lists all installed snaps including their revisions.
- **`awk '/disabled/{print $1, $3}'`**: Filters and prints the name and revision of disabled snaps.
- **`while read snapname revision; do snap remove "$snapname" --revision="$revision"; done`**: Iterates through each disabled snap and removes it.

## Troubleshooting

- **Permission Denied**: If you encounter permission issues, try running the script with `sudo`.
- **Snapd Not Found**: Ensure that Snapd is installed and running on your system.
- **Script Doesn't Run**: Verify that the script has executable permissions and the Bash shell is available.

## Contributing

Contributions to this script are welcome! If you have suggestions or improvements, please feel free to open a pull request or issue on GitHub.

## License

This script is open-source and licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

