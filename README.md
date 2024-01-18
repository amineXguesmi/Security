

# Security Project: Network Services Authentication and Management (2023-2024)

## Overview
A comprehensive initiative project focusing on the configuration and integration of various network services including OpenLDAP, SSH, Apache, OpenVPN, DNS, and Kerberos. The project is structured into three main parts, each addressing different aspects of network services management and authentication mechanisms.

## Objectives

| Part | Description |
|------|-------------|
| Part 1 | Setup and authenticate services with OpenLDAP, SSH, Apache, and OpenVPN. |
| Part 2 | Manage network services with DNS configuration. |
| Part 3 | Implement authentication using Kerberos. |

## Technologies

`OpenLDAP` `SSH` `Apache Server` `OpenVPN` `BIND (DNS)` `Kerberos`

## Project Details

### Part 1: OpenLDAP, SSH, Apache, and OpenVPN Configuration

#### OpenLDAP
- Configure an OpenLDAP server with at least two users and two groups.
- Add x509 certificates and other information for all users.
- Ensure successful user authentication on the OpenLDAP server.
- Test and describe the advantages of LDAP over SSL (LDAPS).

#### SSH Authentication
- Enable SSH authentication via OpenLDAP.
- Restrict SSH access to users in a specific group in OpenLDAP.
- Perform tests with both authorized and unauthorized SSH users.

#### Apache Integration
- Configure Apache to use OpenLDAP authentication.
- Limit web page access to members of a specific group in OpenLDAP.
- Test access with both authorized and unauthorized users.

#### OpenVPN Setup
- Install and configure OpenVPN to use OpenLDAP authentication.
- Test VPN connections using OpenLDAP credentials.
- Conduct tests with both authorized and unauthorized VPN clients.

### Part 2: DNS Server Configuration and Testing

- Set up a DNS (Bind) server on a separate machine.
- Add necessary DNS records for OpenLDAP, Apache, and OpenVPN servers.
- Test DNS resolution for each configured service.
- Ensure domain names associated with services are correctly resolved.

### Part 3: Kerberos Authentication

- Install and configure a Kerberos server.
- Add user principals and password policies.
- Choose one service (OpenLDAP, SSH, Apache, or OpenVPN) for Kerberos authentication integration.
- Document and configure the chosen service to use Kerberos authentication.

## Authors

| Name             | GitHub Profile                                   |
|------------------|--------------------------------------------------|
| Anas Chaibi      | [@AnasChaibi](https://github.com/anasch07)       |
| Firas Mosbahi    | [@FirasMosbahi](https://github.com/FirasMosbahi) |
| Med Amine Guesmi | [@amineXguesmi](https://github.com/amineXguesmi) |
| Adam Fendri      | [@adam-fendri](https://github.com/adam-fendri)   |

