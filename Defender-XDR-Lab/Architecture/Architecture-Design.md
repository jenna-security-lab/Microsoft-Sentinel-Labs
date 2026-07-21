# Architecture Design

## Overview
The environment consists of:
- One Active Directory Domain Controller
- Two Windows 11 user endpoints
- Microft Entra ID tenant
- Microsoft Defender XDR

## Architecture Outline

                                Internet
                                   │
                                   │
                     ┌───────────────────────────┐
                     │   Microsoft 365 Tenant    │
                     │         Entra ID          │
                     │       Defender XDR        │
                     └─────────────┬─────────────┘
                                   │
                        Secure Cloud Connection
                                   │
            ┌──────────────────────┴──────────────────────┐
            │                                             │
    ┌───────────────┐                             ┌───────────────┐
    │  LAB-WIN11-01 │                             │  LAB-WIN11-02 │
    │  Windows 11   │                             │   Windows 11  │
    │ User Endpoint │                             │ User Endpoint │
    │ Defender MDE  │                             │  Defender MDE │
    └───────┬───────┘                             └───────┬───────┘
            │                                             │
            └──────────────────────┬──────────────────────┘
                                   │
                             Domain Network
                                   │
                           ┌───────────────┐
                           │    LAB-DC01   │
                           │ Windows Server│
                           │   Active Dir  │
                           │     DNS       │
                           │  DHCP (opt.)  │
                           └───────────────┘


## Environment Components
|  Device  |  Purpose  |  Notes  |  Example  |
|---|---|---|---|
|  LAB-DC01  |  Active Directory Domain Controller  |  Acts as the company's identity server. Provides user accounts, authentication, group policy, DNS, and domain management.  |  A company employee asks to sign into their laptop. The laptop asks the DC "is John Smith allowed to login?" The DC answers.  |
|  LAB-WIN11-01  |  User Workstation  |  Simulates an employee computer. This device will run Defender, generate security events, receive policies, and simulate normal user activity.  |  Sarah - Accounting  |
|  LAB-WIN11-02  |  User Workstation  |  Simulates a second employee workstation. This device will be used for testing attachs, comparing security events, and generating additional telemetry.  |  Mike - Finance  |
|  Microsoft Entra ID  |  Cloud Identity Provider  |  Acts as my Cloud identity platform. Simulates Microsoft 365 users, Cloud authentication, Conditional Access, and Device Registration  |  N/A  | 
|  Defender XDR  |  Security monitoring platform  |  Acts as my EDR, Investigation platform, and Threat hunting console.  |  It collects process activity, login events, network activity, file changes, and security alerts.  |
