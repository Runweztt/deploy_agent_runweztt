# Attendance Tracker Deployment Agent

Automated shell script for bootstrapping a Student Attendance Tracker project.

## Author
**Name:** Emmanuel .C. Amarikwa  
**GitHub:** runweztt  


## Overview

This script automates the creation of a complete attendance tracking application, demonstrating Infrastructure as Code principles by:
- Creating a standardized directory structure
- Generating all required project files
- Allowing dynamic configuration through user input
- Handling interruptions gracefully with signal traps

## Prerequisites

- Bash shell
- Python 3.x
- `tar` command
- `sed` command

## How to Run the Script

### Basic Usage

1. Clone this repository:
```bash
git clone https://github.com/YourUsername/deploy_agent_YourUsername.git
cd deploy_agent_YourUsername
```

2. Make the script executable:
```bash
chmod +x setup_project.sh
```

3. Run the script:
```bash
./setup_project.sh
```

4. Follow the prompts:
```
Enter project identifier: cs101
Update attendance thresholds? (y/n): n
```

5. Navigate to the created project:
```bash
cd attendance_tracker_cs101
python3 attendance_checker.py
```

### With Custom Configuration

To customize attendance thresholds:
```bash
./setup_project.sh
# Enter project identifier: spring2024
# Update thresholds? y
# Warning threshold: 80
# Failure threshold: 60
```

## How to Trigger the Archive Feature

The archive feature is activated when you interrupt the script using **Ctrl+C**.

### Steps:

1. Start the script:
```bash
./setup_project.sh
```

2. Enter a project identifier when prompted:
```
Enter project identifier: test_archive
```

3. Press **Ctrl+C** at any point during execution

4. The script will automatically:
   - Create a compressed archive: `attendance_tracker_test_archive_archive.tar.gz`
   - Delete the incomplete project directory
   - Display cleanup messages

### Verifying the Archive

Check that the archive was created:
```bash
ls -lh *.tar.gz
```

Extract the archive:
```bash
tar -xzf attendance_tracker_test_archive_archive.tar.gz
cd attendance_tracker_test_archive
```

## Project Structure

The script creates the following structure:

```
attendance_tracker_{identifier}/
├── attendance_checker.py       # Main Python application
├── Helpers/
│   ├── assets.csv             # Student attendance data
│   └── config.json            # Configuration settings
└── reports/
    └── reports.log            # Generated reports
```

## Features

### 1. Directory Automation
- Creates parent directory: `attendance_tracker_{input}`
- Creates subdirectories: `Helpers/` and `reports/`
- Handles existing directory conflicts

### 2. Dynamic Configuration
- Interactive prompts for attendance thresholds
- Input validation (numeric values 0-100)
- Uses `sed` for in-place JSON editing
- Default values: Warning 75%, Failure 50%

### 3. Signal Handling
- Implements trap for SIGINT (Ctrl+C)
- Archives incomplete project state
- Cleans up workspace automatically

### 4. Environment Validation
- Checks for Python 3 installation
- Verifies complete directory structure
- Confirms all required files exist

## Video Walkthrough

[Link to Video Walkthrough]

In this video, I explain:
- My approach to the solution
- How the script was created
- The logic and flow of each function
- Live demonstrations of key features

## Testing

To verify the script works correctly:

1. Test normal execution:
```bash
./setup_project.sh
# Enter: test1, choose: n
cd attendance_tracker_test1
python3 attendance_checker.py
```

2. Test custom configuration:
```bash
./setup_project.sh
# Enter: test2, choose: y, thresholds: 80, 60
cat attendance_tracker_test2/Helpers/config.json
```

3. Test archive creation:
```bash
./setup_project.sh
# Enter: archive_test
# Press Ctrl+C
ls *.tar.gz
```

## Troubleshooting

**Script not executable:**
```bash
chmod +x setup_project.sh
```

**Python not found:**
```bash
# Install Python 3
sudo apt install python3  # Ubuntu/Debian
brew install python3      # macOS
```

**Clean up test files:**
```bash
rm -rf attendance_tracker_*
rm -f *.tar.gz
```

