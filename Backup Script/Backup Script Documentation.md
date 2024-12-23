Automated Backup and Cleanup Script
===================================
Overview

This Bash script automates the process of backing up files from a source directory to a destination directory. It includes optional compression, logging, and automatic cleanup of backups older than 7 days. The script is designed to ensure data safety and minimize manual intervention in backup tasks.
Features

    Validates the existence of source and destination directories.
    Automatically creates the destination directory if it does not exist.
    Backs up files with the following options:
        Uncompressed: Copies files directly to the destination.
        Compressed: Creates a .tar.gz archive.
    Logs all actions in a file (backup.log).
    Cleans up old backups (older than 7 days) to save storage space.

Usage Instructions
1. Prerequisites

    Ensure you have the necessary permissions to read the source directory and write to the destination directory.
    Required tools:
        tar for compression.
        cp for copying files.
        find for cleanup.

2. Script Parameters

The script takes three arguments:

    Source Directory ($1): The directory you want to back up.
    Destination Directory ($2): The directory where the backup will be saved.
    Compression Flag ($3): Optional flag to enable compression (--compress).

3. How to Run the Script

    Make the script executable:

chmod +x <script_name>.sh

Run the script with the required parameters:

./<script_name>.sh <source_directory> <destination_directory> [--compress]

Examples:

    Without compression:

./backup.sh /path/to/source /path/to/destination

With compression:

        ./backup.sh /path/to/source /path/to/destination --compress

Script Workflow
1. Input Validation

    Checks if the source directory exists. If not, logs an error and exits.
    Checks if the destination directory exists. If it doesn't, creates it and logs the action.

2. Backup Process

    Compressed Backup (--compress flag):
        Creates a compressed .tar.gz file in the destination directory.
    Uncompressed Backup (no flag):
        Copies all files from the source to a timestamped subdirectory in the destination.

3. Logging

    Logs all significant actions and errors into backup.log.
    Ensures detailed tracking of the backup process.

4. Cleanup

    Automatically removes:
        Compressed backups (.tar.gz) older than 7 days.
        Uncompressed backup directories (backup_*) older than 7 days.
    Logs the cleanup process.

Log File

    Location: The script writes logs to a file named backup.log in the current directory.
    Log Format: Each log entry includes a timestamp and message.
    Example:

    2024-11-29 14:30:00 - INFO: Created destination directory /path/to/destination.
    2024-11-29 14:35:00 - SUCCESS: Compressed backup created at /path/to/destination/backup_20241129_143000.tar.gz.

Error Handling

    Missing Source Directory:
        Displays an error message and logs the issue.
    Destination Directory Creation Failure:
        Logs the error and exits.
    Backup Failure:
        Logs the failure during compression or file copy.
    Cleanup Errors:
        Logs issues encountered during cleanup of old backups.

Output

    Compressed Backup: A .tar.gz file in the destination directory (e.g., backup_20241129_143000.tar.gz).
    Uncompressed Backup: A directory named backup_<timestamp> in the destination.
