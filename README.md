# Backup
# ASSIGNMENT 1
## AUTOMATED BACKUP FILE

### Working Procedure: 
File Selection: Identifies files with vowels (a, e, i, o, u   small or capital) in their names within the source directory.
Incremental Backup: Copies only files that have been modified (or) newly added since the last backup.
Logging: Logs the process ID (PID), runtime, and the number of files updated to the specified log file.

### Command to run the Script:
`./backup_script.sh -s <source_directory> -d <destination_directory> [-o <output_file>]`

-s <source_directory>: Directory from which files will be backed up.
-d <destination_directory>: Directory where the backup will be stored.
-o <output_file>: (Optional) Log file for storing backup statistics. Default is output.csv.

### CRONJOB
To edit CRONJOB file run this command: 
`crontab -e` 
 
To add the Cron Job to the crontab file to schedule your backup_script.sh: 

`0 0 * * * /path/to/backup_script.sh -s /path/to/source -d /path/to/destination -o /path/to/logfile.csv` 

We have to replace /path/to/backup_script.sh, /path/to/source, /path/to/destination, and /path/to/logfile.csv with the actual paths on system.

To verify whether the CRONJOB is added or not run the command: 
`crontab -l`
