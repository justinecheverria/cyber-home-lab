# Phase 3 - Identity and Access Management

## Overview

This phase of the cybersecurity home lab focused on building an organized identity and access management structure within the `cyberlab.local` Active Directory domain.

Organizational Units (OUs), user accounts, security groups, and a separate privileged administrative account were created to simulate identity management practices used in an enterprise environment.

## Organizational Unit Structure

Custom Organizational Units were created instead of placing all users and computers inside the default Active Directory containers.

The following structure was implemented:

```text
cyberlab.local
│
├── CyberLab-Admins
│
├── CyberLab-Computers
│   ├── Servers
│   └── Workstations
│
├── CyberLab-Groups
│
└── CyberLab-Users
    ├── Finance
    ├── Human Resources
    ├── IT
    └── Sales
```

This structure separates users, computers, security groups, and privileged accounts so that permissions and Group Policies can be managed more effectively.

## User Account Provisioning

Four employee accounts were created to represent different departments within the organization.

| Employee | Username | Department |
|---|---|---|
| Ethan Morales | `emorales` | IT |
| Maya Chen | `mchen` | Finance |
| Jordan Davis | `jdavis` | Human Resources |
| Sofia Martinez | `smartinez` | Sales |

The first employee account was created manually through Active Directory Users and Computers.

The remaining accounts were provisioned using PowerShell and the `New-ADUser` cmdlet. This provided experience with both GUI-based and command-line Active Directory administration.

New users were configured with temporary lab passwords and required to change their password at their next logon.

## Department Security Groups

Global security groups were created for each department:

- `GG-IT`
- `GG-Finance`
- `GG-HR`
- `GG-Sales`

Each employee was assigned to the security group associated with their department.

Using security groups instead of assigning permissions directly to individual users provides a more scalable method of managing access.

For example, access intended for Finance employees can be assigned to `GG-Finance`. Employees can then gain or lose that access simply by changing their group membership.

## Role-Based Access Control

The departmental group structure provides the foundation for role-based access control within the lab.

Users are grouped according to their organizational role rather than being assigned permissions individually.

This approach will later be used when configuring access to resources and applying security controls within the environment.

## Privileged Account Separation

The standard IT account:

`emorales`

was intentionally kept separate from administrative privileges.

A second account was created for privileged administrative activity:

`adm-emorales`

The administrative account is stored inside the `CyberLab-Admins` OU.

Separating standard and privileged accounts reduces the amount of time an administrator operates with elevated permissions and demonstrates the principle of least privilege.

## Administrative Security Group

A dedicated Global Security Group was created:

`GG-IT-Admins`

The `adm-emorales` account was added to this group while the standard `emorales` account was not.

At this stage, `GG-IT-Admins` has not been granted additional administrative permissions. Administrative rights will be assigned deliberately in a later phase of the lab rather than automatically granting broad Domain Administrator privileges.

## PowerShell Administration

PowerShell was used to perform several Active Directory administration tasks, including:

- Creating Active Directory users
- Creating Global Security Groups
- Adding users to security groups
- Verifying user accounts
- Verifying group membership

Example commands used during this phase included:

```powershell
Get-ADUser
New-ADUser
New-ADGroup
Add-ADGroupMember
Get-ADGroupMember
```

Using PowerShell alongside Active Directory Users and Computers provides experience with both manual administration and repeatable command-line management.

## Security Concepts Demonstrated

This phase demonstrates several identity and access management concepts:

- Organizational Unit design
- Active Directory user provisioning
- Security group management
- Role-based access control
- Least privilege
- Separation of standard and privileged accounts
- PowerShell-based Active Directory administration

## Next Phase

The next phase of the lab will introduce a Windows client workstation. The workstation will be connected to the isolated `CYBER-LAB` network, configured to use DC01 for DNS, and joined to the `cyberlab.local` domain.

This will allow the employee accounts created during this phase to authenticate from a domain-joined workstation and will provide the foundation for Group Policy testing.
