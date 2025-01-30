### Backup and Restore Notes
- #### Importance of Backup and Restore
	- **Data Protection**: Ensures data is safe from loss, corruption, or unauthorized access.
	- **Efficiency**: Tools like Rsync, Duplicity, and Deja Dup provide fast and secure backup solutions.
	- **Security**: Encryption tools (e.g., GnuPG, eCryptfs, LUKS) add an extra layer of protection.
- #### Backup Tools in Linux
	1. **Rsync**:
	   - **Purpose**: Efficiently syncs files locally or remotely by transferring only changed portions.
	   - **Installation**:
     ```bash
     sudo apt install rsync -y
     ```
   - **Basic Backup Command**:
     ```bash
     rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
     ```
     - `-a`: Archive mode (preserves permissions, timestamps, etc.).
     - `-v`: Verbose output.
   - **Advanced Options**:
     - **Compression**: `-z` for faster transfers.
     - **Incremental Backups**: `--backup --backup-dir=/path/to/backup/folder`.
     - **Delete Extraneous Files**: `--delete`.
     ```bash
     rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory
     ```
   - **Restore Command**:
     ```bash
     rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory
     ```
2. **Duplicity**:
   - **Purpose**: Adds encryption to Rsync for secure backups.
   - **Use Case**: Ideal for sensitive data stored on remote servers or cloud services.
3. **Deja Dup**:
   - **Purpose**: User-friendly graphical interface for backups.
   - **Features**: Uses Rsync and supports encrypted backups.
- #### Securing Rsync with SSH
	- **Encrypted Transfers**: Use SSH to encrypt data during transfer.
	- **Command**:
  ```bash
  rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
  ```
- **Key-Based Authentication**:
  - Generate SSH key pair:
    ```bash
    ssh-keygen -t rsa -b 2048
    ```
  - Copy public key to remote server:
    ```bash
    ssh-copy-id user@backup_server
    ```
- #### Automating Backups with Cron
	- **Purpose**: Schedule regular backups using cron.
	- **Steps**:
	  1. Create a backup script (`RSYNC_Backup.sh`):
     ```bash
     #!/bin/bash
     rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
     ```
  2. Make the script executable:
     ```bash
     chmod +x RSYNC_Backup.sh
     ```
  3. Add a cron job:
     ```bash
     crontab -e
     ```
     - Add the following line to run the script every hour:
       ```bash
       0 * * * * /path/to/RSYNC_Backup.sh
       ```
- #### Testing Rsync Locally on Pwnbox
	- **Setup**:
	  - Create two directories:
    ```bash
    mkdir to_backup synced_backup
    ```
  - Add sample files to `to_backup`:
    ```bash
    echo "Test file" > to_backup/testfile.txt
    ```
- **Sync Command**:
  ```bash
  rsync -av to_backup/ synced_backup/
  ```
- **Automate with Cron**:
  - Create a script (`local_rsync.sh`):
    ```bash
    #!/bin/bash
    rsync -av to_backup/ synced_backup/
    ```
  - Make it executable:
    ```bash
    chmod +x local_rsync.sh
    ```
  - Add a cron job to run every minute:
    ```bash
    crontab -e
    ```
    - Add:
      ```bash
      * * * * * /path/to/local_rsync.sh
      ```



### Summary
- **Rsync**: Efficient, incremental backups with optional encryption via SSH.
- **Duplicity**: Adds encryption for secure backups.
- **Deja Dup**: User-friendly GUI for backups.
- **Automation**: Use cron to schedule regular backups.
- **Local Testing**: Use Pwnbox to simulate backup and restore processes.
