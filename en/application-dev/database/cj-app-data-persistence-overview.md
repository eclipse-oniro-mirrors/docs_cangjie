# Overview of Application Data Persistence

Application data persistence refers to the process of saving data from memory to a device in the form of files or databases. Data in memory typically exists as arbitrary data structures or objects, while data on storage media may take forms such as text, databases, or binary files.

The OpenHarmony standard system supports typical data storage forms, including user preferences, key-value databases, and relational databases.

Developers can choose the appropriate data storage form based on the following functional descriptions to meet their application's data persistence needs.

- **Preferences:** Typically used to store application configuration information. Data is saved on the device in text form, and during application usage, the entire text data is loaded into memory. This results in fast access and high efficiency but is unsuitable for scenarios requiring storage of large amounts of data.
- **KV-Store:** A non-relational database where data is organized, indexed, and stored in "key-value" pairs, with the "key" serving as a unique identifier. It is suitable for storing business data with minimal data or business relationships. Additionally, it is widely used because it reduces the complexity of resolving database version compatibility issues and conflict resolution during data synchronization in distributed scenarios. Compared to relational databases, it is easier to achieve cross-device and cross-version compatibility.
- **RelationalStore:** A relational database that stores data in rows and columns, widely used for handling relational data in applications. It includes a series of interfaces for operations such as insert, delete, update, and query. Developers can also execute custom SQL statements to meet the needs of complex business scenarios.