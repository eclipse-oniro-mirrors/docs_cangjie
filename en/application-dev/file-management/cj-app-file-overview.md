# Application Files Overview  

Application Files: Files owned by applications, including installation files, resource files, cache files, etc.  

- Data used and stored by applications on the device is saved in an application-specific directory in the form of files, key-value pairs, databases, etc. This dedicated directory is called the "Application Files Directory," where all data is stored in various file formats. These files are referred to as application files.  

- The "Application Files Directory" and a subset of system files (essential system files required for application operation) form a collection called the "Application Sandbox Directory," representing the entire directory scope visible to the application. Therefore, the "Application Files Directory" resides within the "Application Sandbox Directory."  

- System files and their directories are read-only for applications. Applications can only save files under the "Application Files Directory" and must choose appropriate subdirectories for data storage based on usage guidelines and considerations.  

The following sections will provide detailed explanations of the application sandbox, application files directory, application file access and management, application file sharing, and related topics.