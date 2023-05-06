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



## <a name=""></a>📖 Auditing



## <a name=""></a>📖 Best Practices




