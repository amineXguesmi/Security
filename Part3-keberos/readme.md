
# Kerberos Server Configuration 

## Introduction
This guide outlines the steps for configuring a Kerberos server and a client machine. Kerberos is a network authentication protocol that uses tickets to allow nodes to prove their identity in a secure manner.

## Prerequisites
- Two machines (one for the server, one for the client)
- Operating System: Ubuntu or similar Linux distribution
- Sudo privileges on both machines

## Configuration Steps

### Step 1: Setting Hostnames and FQDN
- Set the hostname on the server and client machines:
   - Server: `sudo hostname set-hostname kdc.insat.tn`
   - Client: `sudo hostname set-hostname client.insat.tn`
- Modify the `/etc/hosts` file on both machines to ensure proper name resolution.
   - ![Hosts File Server](images/Untitled.png)
   - ![Hosts File Client](images/Untitled%201.png)

### Step 2: Installing Kerberos Packages
- Install Kerberos packages on the server and client machines:
  ```bash
  sudo apt install krb5-kdc krb5-admin-server krb5-config
  ```
   - ![Kerberos Package Installation](images/Untitled%202.png)
     ... [Other installation images]

### Step 3: Configuring Kerberos
1. **View and Edit Kerberos Configuration Files**
   - View the contents of `/etc/krb5.conf`.
     ![Krb5.conf](images/Untitled%205.png)
   - Create a new Realm.
     ![New Realm](images/Untitled%206.png)
   - Modify `/etc/krb5kdc/kadm5.acl`.
     ![Kadm5.acl Modification](images/Untitled%207.png)
     ... [Continue with other relevant images]

2. **Creating Principals**
   - Use `kadmin.local` to create various principals including `root/admin` and host principals.
     ![Creating Principals](images/Untitled%209.png)
     ... [Continue with other relevant images]

### Step 4: Managing Keytabs
- Add entries in the keytab file and verify them.
  ![Keytab Addition](images/Untitled%2014.png)
  ... [Continue with other keytab images]

### Step 5: Configuring OpenSSH with Kerberos
1. **Install OpenSSH Server:**
   ```bash
   sudo apt install openssh-server
   ```
   Configure `/etc/ssh/sshd_config` and `/etc/ssh/ssh_config` for Kerberos authentication.
   ![SSH Configuration](images/Untitled%2020.png)
   ... [Continue with other SSH configuration images]

2. **Install krb5-user Package:**
   ```bash
   sudo apt install krb5-user
   ```
![krb5-user Installation](images/Untitled%2023.png)
![krb5-user Installation](images/Untitled%2024.png)
![krb5-user Installation](images/Untitled%2025.png)

 

