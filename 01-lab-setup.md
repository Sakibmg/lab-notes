# My Lab Setup

## Goal
A safe, isolated environment to practise security skills on my own machines.

## Components
- Host: Windows laptop running VirtualBox
- Attacker: Kali Linux VM
- Target: Metasploitable2 (deliberately vulnerable Linux VM)
- Windows AD lab: coming next

## Network
Kali and Metasploitable are on a private virtual network. The target is never on my real Wi-Fi network (no bridged mode).

## What I verified
- Kali can ping the target
- nmap -sV lists the target's open services
- My own Python scanner finds the same open ports as nmap

## Lessons
- A powered-off target looks like a network fault: connect_ex returned 11 and ping said "Destination Host Unreachable". Check the VM is running first.
- Snapshots before changes let me undo mistakes.

## Active Directory Lab (added)

- DC01: Windows Server 2022 (Desktop Experience), promoted to a Domain Controller for a new forest, corp.local
- WS01: a second Windows Server 2022 VM, joined to corp.local as a domain member
- Both VMs run on an isolated Internal Network (labnet) in VirtualBox, with no internet access and no connection to my real network — deliberate, since a domain controller should never be exposed
- Static IPs: DC01 = 192.168.10.10 (also runs DNS for the domain), WS01 = 192.168.10.20
- Created an Organizational Unit (LabUsers) with two test accounts for later attack scenarios (Kerberoasting, BloodHound in Week 6)
- Verified the domain join from both sides: WS01 reports corp.local as its domain, and WS01 appears under Computers in Active Directory Users and Computers on DC01
