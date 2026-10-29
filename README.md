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
