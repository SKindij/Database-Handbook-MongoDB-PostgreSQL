# 📚 MongoDB Security
&ensp; Security is crucial for protecting your data and keeping unauthorized access at bay.

## <a name=""></a>📖 Authentication
&ensp; It involves verifying the identity of users or applications trying to access the database.\
MongoDB supports several authentication mechanisms, including:
+ SCRAM (Salted Challenge Response Authentication Mechanism): 
  * it is the default authentication mechanism in MongoDB;
  * it uses a username and password to authenticate users.
+ x.509 certificates: 
  * use it for authentication, where clients present a valid certificate.
+ LDAP (Lightweight Directory Access Protocol): 
  * MongoDB can integrate with LDAP servers for authentication purposes.

&ensp; When setting up authentication, it is crucial to create strong passwords, avoid using default credentials, and regularly rotate passwords to enhance security.

## <a name=""></a>📖 Authorization
&ensp; It determines the level of access users or applications have to the database and its resources. MongoDB provides flexible authorization controls using Role-Based Access Control (RBAC).\
Key concepts to understand include:
+ Roles: 
  * built-in like read, readWrite, and userAdmin;
  * you can create custom roles;
+ Privileges: 
  * they are granular permissions that can be assigned to roles;
  * they include actions such as find, insert, update, remove, and more.
+ Role-Based Access Control:
  * RBAC allows you to assign roles to users or applications, controlling what operations they can perform.

&ensp; By properly configuring authorization, you can limit access to sensitive data and ensure that users have only the necessary permissions.


## <a name=""></a>📖 Encryption
&ensp; It helps protect data stored in MongoDB, both at rest and during transit. MongoDB provides the following encryption options:
+ TLS/SSL: 
  * Transport Layer Security (TLS) or Secure Sockets Layer (SSL) can be used to encrypt communication between the MongoDB client and server, ensuring data integrity and confidentiality during transit.
+ Encryption at Rest: 
  * MongoDB Enterprise offers the ability to encrypt data on disk using native encryption. 
  * This feature encrypts the data files and their backups, providing an additional layer of security.

&ensp; Properly implementing encryption measures helps safeguard data from unauthorized access, both while in transit and when stored on disk.


## <a name=""></a>📖 Auditing
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


## <a name=""></a>📖 Best Practices




