## Section 1

### Statement

`Section 1: OpenLDAP Configuration`

1. Configure an OpenLDAP server with at least two users and two groups.
2. Add information of your choice, including x509 certificates for all users.
3. Ensure that users can successfully authenticate on the OpenLDAP server.
4. Test the secure LDAP part with LDAPS and describe the various advantages.

### Practice

#### Installation and Configuration of OpenLDAP

1. **Install OpenLDAP and utilities**:

   ```bash
   sudo apt-get update
   sudo apt-get install slapd ldap-utils
   ```

2. **Reconfigure OpenLDAP** (set the domain and admin password):

   ```bash
   sudo dpkg-reconfigure slapd
   ```

   - Answer the reconfigure questions:
      - Domain: www.insatGl4.tn
      - Organization Name: insatGl4.tn
      - Remove the database when purging slapd: No

#### Creating LDAP Structure

1. **Create a basic LDIF file** (`base.ldif`):

   - This file should contain your domain components and organizational units.
   - Example content for `base.ldif`:

     ```ldif
     dn: ou=users,dc=www,dc=insatGl4,dc=tn
     objectClass: organizationalUnit
     ou: users

     dn: ou=groups,dc=www,dc=insatGl4,dc=tn
     objectClass: organizationalUnit
     ou: Groups
     ```

2. **Add the basic structure to LDAP**:

   ```bash
   ldapadd -x -D cn=admin,dc=www,dc=insatGl4,dc=tn -W -f base.ldif
   ```

#### Adding Users and Groups

1. **Create a users LDIF file** (`users.ldif`):

   - Define user attributes (e.g., `cn`, `sn`, `uid`).
   - Example content for `users.ldif` for two users (`user1` and `user2`):

     ```ldif
     dn: cn=Souheib,ou=users,dc=www,dc=insatGl4,dc=tn
     objectClass: inetOrgPerson
     uid: souheib
     sn: Souheib
     cn: Souheib
     userPassword: root

     dn: cn=Samir,ou=users,dc=www,dc=insatGl4,dc=tn
     objectClass: inetOrgPerson
     uid: samir
     sn: Samir
     cn: Samir
     userPassword: root
     ```

2. **Add users to LDAP**:

   ```bash
   ldapadd -x -D cn=admin,dc=www,dc=insatGl4,dc=tn -W -f users.ldif
   ```

3. **Create a groups LDIF file** (`groups.ldif`):

   - Define group attributes (e.g., `cn`, member `uid`).
   - Example content for `groups.ldif` for two groups (`group1` and `group2`):

     ```ldif
     dn: cn=professors,ou=groups,dc=www,dc=insatGl4,dc=tn
     objectClass: groupOfNames
     cn: professors
     member: uid=souheib,ou=users,dc=www,dc=insatGl4,dc=tn

     dn: cn=ad,ou=groups,dc=www,dc=insatGl4,dc=tn
     objectClass: groupOfNames
     cn: ad
     member: uid=samir,ou=users,dc=www,dc=insatGl4,dc=tn
     ```

4. **Add groups to LDAP**:

   ```bash
   ldapadd -x -D cn=admin,dc=www,dc=insatGl4,dc=tn -W -f groups.ldif
   ```

#### Managing x509 Certificates with OpenSSL

1. **Generate the CA key and certificate**:

   ```bash
   openssl genrsa -out ca.key 4096
   openssl req -new -x509 -days 3650 -key ca.key -out ca.crt
   ```

2. **Generate user keys and certificates** (for `user1` and `user2`):

   ```bash
   openssl genrsa -out souheib.key 2048
   openssl req -new -key souheib.key -out souheib.csr
   openssl x509 -req -days 365 -in souheib.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out souheib.crt

   openssl genrsa -out samir.key 2048
   openssl req -new -key samir.key -out samir.csr
   openssl x509 -req -days 365 -in samir.csr -CA ca.crt -CAkey ca.key -set_serial 02 -out samir.crt
   ```

3. **Update users with x509 certificates**:

   - Update the `users.ldif` file to include user certificates (use the actual Base64 content of the `.base64` files).

4. **Apply the updates to LDAP**:

   ```bash
   ldapmodify -x -D cn=admin,dc=www,dc=insatGl4,dc=tn -W -f update_users.ldif
   ```

### Configuration Verification

1. **LDAP Tree Verification**:

   ```bash
   ldapsearch -x -D cn=admin,dc=www,dc=insatGl4,dc=tn -W -b "dc=www,dc=insatGl4,dc=tn" -s sub -a always "(objectclass=*)"
   ```

2. **Authentication Testing**:

   - Use the `ldapwhoami` command to test authentication for each user:

     ```bash
     ldapwhoami -x -D "cn=souheib,ou=users,dc=www,dc=insatGl4,dc=tn" -W
     ldapwhoami -x -D "cn=samir,ou=users,dc=www,dc=insatGl4,dc=tn" -W
     ```

### Implementing LDAPS (LDAP over SSL)

#### Configuring LDAP to Use SSL

1. **Configure SSL for OpenLDAP**:

   - Edit the OpenLDAP configuration file to enable LDAPS. You need to specify the paths to your SSL certificates.

     ```bash
     sudo nano /etc/ldap/slapd.conf
     ```

   - Add the following lines:

     ```
     TLSCACertificateFile /ssl/ca.crt
     TLSCertificateFile /ssl/ldapserver.crt
     TLSCertificateKeyFile /ssl/ldapserver.key
     ```

   - Restart OpenLDAP to apply the changes:

     ```bash
     sudo service slapd restart
     ```

2. **Verify LDAPS connection**:

   - Use the following command to test the secure connection:

     ```bash
     ldapsearch -x -H ldaps://192.168.56.102 -b "dc=www,dc=insatGl4,dc=tn" -D "cn=admin,dc=www,dc=insatGl4,dc=tn" -W
