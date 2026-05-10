# Windows Baseline Configuration Snapshot Collector
## CYB 125 Final Project — Part 1: Project Plan

**Student name:** Ewan Cordice
**Date:** May 9, 2026

---

## About this Project

I am creating a Python script that takes a snapshot of your Windows VM configuration and stores it in a JSON file. A security analyst can later compare that snapshot with a newer one from the same machine to spot any changes that should not have happened. This process is known as system baselining. It is one of the most effective defensive measures a small security team can put in place.

---

## Approach

I will gather data from three categories of sources:

- Windows Registry (read with the `winreg` Python module)
- Performance counters (sampled with the `typeperf` command)
- Command-line utilities (invoked from Python with `subprocess`)

---

## Data Dictionary

The program will rely on a single main dictionary, often named system_snapshot, which organizes all configuration data collected from the Windows machine. At the top level, this dictionary includes keys for the hostname, operating system details, hardware specifications, network configuration, installed software, system services, and a timestamp marking when the snapshot was taken. Each of these keys either stores a simple value like the hostname or timestamp or points to a nested dictionary or list that captures more detailed information.
Within these nested structures, the os_info section records the OS name, version, build number, and architecture. The hardware section stores CPU details, core count, total memory, and a list of disk entries, each containing device name, size, and free space. The network section contains a list of network adapters, with each entry describing the adapter’s name, MAC address, IP addresses, and status. Installed software and services are represented as lists of dictionaries, where each item includes fields such as name, version, publisher, status, and startup type. Together, these nested keys create a complete, structured snapshot that can be compared against future system states to detect unauthorized changes.



---

## Configuration Areas

### 1. snapshot_metadata
This records when and how the snapshot was taken so you always know the context of the data you’re comparing.

### 2. system_identity
This captures the machine’s name and basic identity so you can confirm which system the baseline belongs to.

### 3. hardware_profile
This logs CPU, memory, and disk details so you can detect unexpected hardware changes or resource issues.

### 4. network_configuration
This shows IP settings and network adapters so you can spot unauthorized network changes that could expose the system.

### 5. listening_ports
This lists which ports the system is accepting connections on so you can catch suspicious or newly opened entry points.

### 6. local_user_accounts
This tracks all local accounts so you can detect unauthorized users or privilege changes.

### 7. password_policy
This records password rules so you can verify the system is enforcing strong security requirements.

### 8. auto_start_services
This shows which services launch at boot so you can identify persistence mechanisms or unwanted software.

### 9. running_processes
This captures what is actively running so you can detect unusual or malicious processes.

### 10. installed_software
 This lists all installed programs so you can spot unauthorized or risky applications.

### 11. installed_hotfixes
 This shows which security patches are applied so you can confirm the system is properly updated.

### 12. persistence_locations
This checks common places malware hides to stay running so you can detect suspicious entries early.

### 13. scheduled_tasks
This records automated tasks so you can identify hidden jobs that might be malicious or unnecessary.

### 14. security_posture
This summarizes key security settings so you can quickly see whether the system meets your security standards.

### 15. performance_snapshot
This captures CPU, memory, and disk usage so you can compare performance over time and detect anomalies.

### 16. network_shares
 This lists shared folders so you can ensure sensitive data isn’t being exposed to the wrong users.

---

## Strategy

I am planning to use AI as a learning partner for this project, not as a shortcut to avoid understanding the code. I will ask questions that help me think, such as how to structure a function, why a certain Windows API behaves a certain way, or the best way to understand a specific type of system data.
 I would not ask it to write the entire script for me. When it does help generate small code snippets, I will verify them by testing each part in my VM, checking the documentation, and making sure I understand every line before keeping it.
 AI will be most useful when I am figuring out how to gather system information. It will be least helpful during the final cleanup stages, where I want to rely on my own judgment to make the code readable.


Three prompts I plan to use:

1. How can I test the places where malware usually hides to make sure my script is really checking them correctly?
2. What is the simplest and safest way to list local user accounts without breaking anything or needing too many permissions?
3. Can you walk me through how to compare two snapshots so I only see the important differences and not a bunch of noise?

---

## Milestones

The project is structured around eight milestones, each one designed to produce a working JSON file with an additional section implemented. The milestone structure isn't just a grading convenience, it's a deliberate AI-collaboration pattern. 

When students use AI well, they treat it like a pair programmer: they bring it small, well-scoped problems, ask it to explain things rather than just produce things, and verify its answers against an authoritative source (the textbook, the official Python docs, or their own running code). The output is code they understand and could rewrite from scratch.

The eight-milestone structure exists to force responsible AI usage. Each milestone is small enough that you can hold the whole thing in your head. Each milestone has a specific Python concept attached to it, so you know what you're supposed to be learning. Each milestone has a suggested AI prompt that asks for explanation, not code.

Your goal is not to finish the project as fast as possible. Your goal is to finish the project understanding what you built. Those are different goals. The milestone structure pushes you toward the second one.



---

## Notes for the Instructor
Anything you want to put here...