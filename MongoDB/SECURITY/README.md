# 📚 MongoDB Security
&ensp; Security is crucial for protecting your data and keeping unauthorized access at bay.

## <a name="authentication"></a>📖 Authentication
&ensp; It involves verifying the identity of users or applications trying to access the database.\
MongoDB supports several authentication mechanisms, including:
+ **SCRAM (Salted Challenge Response Authentication Mechanism):** 
  * it is the default authentication mechanism in MongoDB;
  * it uses a username and password to authenticate users.
+ **x.509 certificates:**
  * use it for authentication, where clients present valid certificate;
  * enables clients to verify each other’s authenticity using public key infrastructure (PKI);
  * > implementing
    - **Obtain Certificates:**\
      > _Get an X.509 certificate (issued by single Certificate Authority) for server and each client that connects to MongoDB server._
    - **Configure MongoDB Server**: 
      > _To enable X.509 authentication, you’ll need to start MongoDB with following options:_\
      > `mongod --tlsMode requireTLS --tlsCertificateKeyFile /path/to/server.pem --tlsCAFile /path/to/ca.pem --auth`
    - **Create the User Administrator:**\
      > _Use following command on admin database:_
      > ``` javascript
      >  db.getSiblingDB('$external').runCommand({
      >    createUser:
      >      'C=US,ST=New York,L=New York City,O=MongoDB,OU=kerneluser,CN=client@example.com',
      >    roles: [
      >      { role: 'userAdminAnyDatabase', db: 'admin' },
      >     { role: 'clusterAdmin', db: 'admin' },
      >      { role: 'readWriteAnyDatabase', db: 'admin' },
      >      { role: 'dbAdminAnyDatabase', db: 'admin' },
      >    ],
      >    writeConcern: { w: 'majority', wtimeout: 5000 },
      >  });
      >  ```
    - **Authenticate with the Client Certificate:**\
      > _use mongo shell command that includes client certificate and CA certificate files:_
      > `mongo --tls --tlsCertificateKeyFile /path/to/client.pem --tlsCAFile /path/to/ca.pem --authenticationDatabase '$external' --authenticationMechanism 'MONGODB-X509' --host hostname.example.com`
+ **LDAP (Lightweight Directory Access Protocol):**
  * MongoDB can integrate with LDAP servers for authentication purposes.
  * It is application protocol used for accessing and managing distributed directory information services over network.
  * LDAP Proxy Authentication adds additional layer of security and simplifies user management process. 
  * It allows MongoDB to delegate authentication process to LDAP server without storing user credentials in MongoDB server.



&ensp; When setting up authentication, it is crucial to create strong passwords, avoid using default credentials, and regularly rotate passwords to enhance security.

## 📖 Authorization
&ensp; It determines level of access users or applications have to database and its resources. MongoDB provides flexible authorization controls using **Role-Based Access Control** (RBAC - allows you to assign roles to users or applications, controlling what operations they can perform.).

&ensp; Each role consists of a set of privileges that determine the user’s abilities within the system. MongoDB has several built-in roles, and you also have the option to create custom roles as needed. By assigning the appropriate roles to users, you can limit their access to various parts of the database and protect sensitive information.

#### Built-in Roles
* dbAdminAnyDatabase: Allows administrative tasks for all databases except for the local and config;
* dbAdmin: allows administrative tasks, such as managing indexes and user-defined roles, for specified database;
* userAdminAnyDatabase: allows managing user access for all databases except for local and config;
* userAdmin: allows managing user access for specified database;
* ClusterAdmin: allows administrative tasks for entire cluster, such as configuring replica sets and sharding;
* Read: allows read operations on specified database;
* ReadWrite: allows read and write operations on specified database;
* ReadAnyDatabase: allows read operations on all databases except for local and config;
* ReadWriteAnyDatabase: allows read and write operations on all databases except for local and config;

#### Custom Roles
&ensp; You can create custom roles to cater to specific requirements of your application. Custom roles can have any combination of built-in roles’ privileges and user-defined actions.

> _Here’s an example:_
> > ```javascript
> >  use witcherWorld_db;
> >  
> >  db.createRole({
> >    role: 'readMonsters',
> >    privileges: [
> >      {
> >        resource: { db: 'witcherWorld_db', collection: 'monsters' },
> >        actions: ['find', 'aggregate'],
> >      },
> >    ],
> >    roles: [],
> >  });
> > ```

#### Assigning Roles to Users
&ensp; To ensure that users have the appropriate level of access and permissions, you assign specific roles to them. 

> _Here’s an example:_
> > ```javascript
> >  db.createUser({
> >    user: 'geralt77',
> >    pwd: 'password123',
> >    roles: [
> >      { role: 'readMonsters', db: 'witcherWorld_db' },
> >      { role: 'read', db: 'witcherWorld_db' },
> >    ],
> >  });
> > ```

&ensp; _By properly configuring authorization, you can limit access to sensitive data and ensure that users have only the necessary permissions._


## <a name="encryption"></a>📖 Encryption
&ensp; It helps protect data stored in MongoDB, both at rest and during transit. MongoDB provides the following encryption options:
+ TLS/SSL: 
  * Transport Layer Security (TLS) or Secure Sockets Layer (SSL) can be used to encrypt communication between the MongoDB client and server, ensuring data integrity and confidentiality during transit.
+ Encryption at Rest: 
  * MongoDB Enterprise offers the ability to encrypt data on disk using native encryption. 
  * This feature encrypts the data files and their backups, providing an additional layer of security.

&ensp; Properly implementing encryption measures helps safeguard data from unauthorized access, both while in transit and when stored on disk.


## 📖 Auditing
&ensp; It involves monitoring and recording activities within a MongoDB deployment. MongoDB provides auditing features that allow you to track events such as authentication attempts, database operations, and system activities.\
Some key auditing capabilities include:
+ Audit Logs: 
  * MongoDB can generate detailed audit logs containing information about authentication, authorization, and other activities. 
  * These logs can be used for compliance, troubleshooting, and security analysis.
+ Fine-Grained Auditing: 
  * MongoDB allows you to configure audit filters to focus on specific events or activities of interest, enabling more targeted auditing.
+ Integration with SIEM Tools: 
  * MongoDB audit logs can be integrated with Security Information and Event Management (SIEM) tools for centralized monitoring and analysis.

&ensp; By enabling auditing, you can gain visibility into your MongoDB deployment, detect suspicious activities, and meet regulatory compliance requirements.


## <a name="practices"></a>📖 Best Practices
+ Keep MongoDB Updated: 
  * Stay up to date with the latest MongoDB versions, as they often include security patches and improvements.
+ Secure Network Access: 
  * Limit network access to MongoDB servers using firewalls or network security groups. 
  * Allow only trusted connections from authorized sources.
+ Use Strong Authentication: 
  * Enforce strong passwords, avoid default credentials, and enable multi-factor authentication (MFA) to provide an extra layer of security.
+ Apply Least Privilege: 
  * Follow the principle of least privilege by granting users or applications only the necessary permissions required to perform their tasks. 
  * Avoid assigning overly permissive roles.
+ Enable Encryption: 
  * Implement TLS/SSL encryption for communication between clients and the MongoDB server. 
  * Additionally, consider enabling encryption at rest to protect data stored on disk.
+ Regularly Back up Data: 
  * Perform regular backups of your MongoDB data and ensure the backups are securely stored. 
  * This helps in case of data loss or security incidents.
+ Monitor and Audit: 
  * Enable auditing and monitor MongoDB logs to detect any suspicious activities or unauthorized access attempts. 
  * Regularly review and analyze audit logs for security analysis.
+ Secure Deployment: 
  * Follow security best practices for the overall deployment, including keeping the server and operating system patched, using secure network configurations, and employing intrusion detection and prevention systems.
+ Educate Users: 
  * Train and educate users on best practices for handling sensitive data, password management, and recognizing potential security threats such as phishing attempts.
+ Regularly Perform Security Assessments: 
  * Conduct security assessments, such as vulnerability scanning and penetration testing, to identify and address any security weaknesses in your MongoDB deployment.

&ensp; It's important to note that security is an ongoing process, and you should stay updated with the latest security practices, monitor security advisories, and continuously evaluate and improve the security measures implemented in your MongoDB environment.

&ensp; By implementing these best practices, you can strengthen the security of your MongoDB deployment and protect your data from potential threats.
