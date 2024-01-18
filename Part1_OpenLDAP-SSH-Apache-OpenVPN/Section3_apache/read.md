 1-**Install Apache2:**
    
    - Screenshot
        
        ![Untitled](pics/Untitled%2030.png)
        
    
    2-**Enable required modules** `mod_ldap` and `mod_authnz_ldap` and restart apache
    
    - Screenshot
        
        ![Untitled](pics/Untitled%2031.png)
        
    
    3-**Configure LDAP Authentication for a Directory or Location**:
    
    3.1- Create a “protected” directory in /var/www/html and add a html file:
    
    - Screenshot
        
        ![Untitled](pics/Untitled%2032.png)
        
    - Screenshot
        
        ![Untitled](pics/Untitled%2033.png)
        
    
    3.2- Configure the config file for Ldap authentication:
    
    - Screenshot
        
        ![Untitled](pics/Untitled%2034.png)
        
    - Screenshot
        
        ![Untitled](pics/Untitled%2035.png)
        
    
    • `AuthType Basic`: Specifies the type of authentication. We use Basic here.
    
    • `AuthName`: This text will be displayed on the login prompt.
    
    • `AuthBasicProvider ldap`: Specifies that the LDAP provider is used for basic authentication.
    
    • `AuthLDAPURL`: Specifies the URL of your LDAP server. This includes the server address, the base DN to search.
    
    Our configuration here is for group authentication
    
    4-Testing:
    
    To test our work we just head to the requested site where will be asked to enter our user and password information
    
    - Screenshot
        
        ![Untitled](Security%20GL4%202b4a1420bcc445e480f013d3f3de320b/Untitled%2036.png)
