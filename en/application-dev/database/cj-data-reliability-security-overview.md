# Overview of Data Reliability and Security  

## Functional Scenarios  

During system operation, storage corruption, insufficient storage space, file system permissions, and power failures may cause database failures. For example, corruption of the contacts application database may result in the loss of user contacts; corruption of the calendar application database may lead to missed calendar reminders. To address these issues, data management provides solutions and capabilities related to data reliability and security.  

- **Backup and Recovery**: For critical business applications (e.g., banking), data loss or severe anomalies can be mitigated by restoring the database from a backup, ensuring that key data is not lost.  
- **Database Encryption**: When storing highly sensitive information such as authentication credentials or financial data, databases can be encrypted to enhance security.  
- **Database Classification and Grading**: During cross-device data synchronization, data management enforces access control based on data security labels and device security levels to ensure data security.  
- **Class E Encrypted Databases**: Applications storing sensitive user information should use Class E databases. When the device is locked and certain conditions are met, the encryption key is destroyed, rendering Class E databases inaccessible. After unlocking, the key is restored, and normal read/write operations resume, thereby safeguarding sensitive information.  

Additionally, backup databases are stored within the application's sandbox. If storage space is insufficient, local database backups can be deleted to free up space.  

## Basic Concepts  

Before developing features related to data reliability and security, familiarize yourself with the following concepts.  

### Database Backup and Recovery  

- **Database Backup**: Refers to creating a complete backup of the current database file. OpenHarmony database backups involve a full backup of all database files. The database does not need to be closed during backup; simply call the backup interface to complete the process.  
- **Database Recovery**: Restores the current database file from a specified backup file. Upon completion, the current database data will match the state of the specified backup file.  

### Database Encryption  

Database encryption involves encrypting the entire database file, enhancing security and effectively protecting its contents.  

### Database Classification and Grading  

Distributed data management implements classification and grading for data protection, providing access control mechanisms based on data security labels and device security levels.  

Higher data security labels and device security levels correspond to stricter encryption and access control measures, resulting in greater data security.  

## Operational Mechanisms  

### Database Backup and Recovery Mechanism  

During backup, the current database is saved to a specified file. Subsequent operations on the database do not affect the backup file. Only when recovering from a specified backup file will the backup overwrite the current database, enabling data rollback.  

- **Key-Value Database Backup Path**: `/data/service/el1(el2)/public/database/...{appId}/kvdb/backup/...{storeId}`  
- **Relational Database Backup Path**: `/data/app/el1(el2)/100/database/...{bundlename}/rdb`  

### Database Encryption Mechanism  

In OpenHarmony, developers do not need to provide encryption keys for database encryption. Instead, they only need to set the encryption state of the database. The system automatically handles encryption using the [HUKS Universal Keystore System](../../../en/application-dev/reference/UniversalKeystoreKit/cj-apis-security_huks.md), generating and protecting the database encryption key.  

## Constraints  

- Database encryption keys are automatically replaced once a year.  
- A maximum of 5 backups can be created for key-value databases.  
- Automatic backups for key-value databases require the device to be in a screen-off and charging state.