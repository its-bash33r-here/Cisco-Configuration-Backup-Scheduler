# Cisco-Configuration-Backup-Scheduler
This project automates the process of backing up Cisco device configurations using Kron and archiving the backups to a secure location.

**Objectives:**

- Schedule regular backups of Cisco device configurations
- Securely store backups in an archive
- Simplify configuration management and disaster recovery

**Technologies:**

- Cisco IOS
- Kron
- TFTP (Optional)

**Implementation:**

1. **Create a Kron Policy List:**

Define a Kron policy list that specifies the backup commands to be executed at scheduled intervals. This policy list should include the following commands:

```
copy running-config startup-config
archive config path flash:config-backup/config-backup-$(date +"%Y-%m-%d").cfg
```

2. **Configure Kron Occurrence:**

Apply the Kron policy list to a global Kron occurrence. This occurrence determines the frequency of the backups. For instance, to perform daily backups at 12:00 AM, use the following configuration:

```
kron occurrence config 1 policy-list backup
cron occurrence config 1 start-time 00:00:00
kron occurrence config 1 end-time 23:59:59
cron occurrence config 1 run-days mon-sun
```

3. **Optional: Archiving Backups to a Remote Server:**

If you want to archive backups to a remote server, you can use TFTP or another file transfer protocol. Modify the Kron policy list to transfer the backup file to the remote server.

```
copy running-config startup-config
copy flash:config-backup/config-backup-$(date +"%Y-%m-%d").cfg tftp://remote_server_ip/config_backup/
```

4. **Verify Backup Operation:**

Confirm that the backups are being executed successfully by monitoring the archive directory or remote server.

**Benefits:**

- Automated and regular backups ensure data integrity and protection against configuration loss.
- Secure archiving prevents unauthorized access to sensitive configuration data.
- Simplified configuration management facilitates change tracking and rollback.
- Enhanced disaster recovery capabilities enable rapid restoration of network operations.

**Additional Notes:**

- This project is intended for Cisco devices running IOS or NX-OS.
- Kron is a command scheduler built into Cisco IOS and NX-OS.
- Archiving backups to a remote server provides an extra layer of protection in case of device failure.

By implementing this project, you can streamline configuration management, safeguard critical data, and streamline disaster recovery procedures for your Cisco network infrastructure.
