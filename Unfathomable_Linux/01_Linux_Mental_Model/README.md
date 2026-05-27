# Kernel vs Distribution vs WSL2

## 1. Linux Kernel:

- The brain of the OS
- It manages CPU, memory, devices, networking.
- It's just a program.

## 2. Distribution (Ubuntu):

- Kernel + All User tools (like shell, package manager, systemd). Companies standardize on Ubuntu LTS because it's stable for 5 Years.

## 3. WSL2

- A real linux kernel running inside a light weight VM on windows. It is extremely close to a real cloud VM.

---

## Three ways to see the System Info.

![alt text](images/System_Info.PNG)

---

### Production rule: No mouse. No GUI. No Windows File Explorer for anything inside Linux.

![alt text](images/CLI_Info.PNG)

---

## 3. Core Commands you will use every single day

### 3.1 PWD (Print Working Directory)

Syntax : > pwd

Why : > You SSH into a server 3:00 AM - first command you run

Production Use : > Always know where you are.

![alt text](images/PWD_command.PNG)

---

### 3.2 ls (List (the #1 command in Linux history)

- long format (permissions, owner, size, date)
  ![alt text](images/ls_Long_Format.PNG)

- show hidden files (dot files)
  ![alt text](images/ls_Show_Hidden_Files.PNG)

- human-readable sizes (K, M, G) ← use this in prod
  ![alt text](images/ls_Human_Readable.PNG)

- sort by size (largest first)
  ![alt text](images/ls_Sort_By_Size.PNG)

- sort by modification time (newest first)
  ![alt text](images/ls_Sort_By_Modification_Time.PNG)

- combination you will type 1000 times in your career
  ![alt text](images/ls_Sort_By_Modification_Time_With_Human_Redable.PNG)

---

## 4. CD (Change Directory)

- First moved to /etc folder, and then come back to home directory.
  ![alt text](images/cd_movments_1.PNG)

#### Pro tip: Tab completion is your superpower. Type cd /et → press Tab twice → see options.

- Back to previous directory (super useful!) (How to Go Previous one)
  ![alt text](images/cd_movments_2.PNG)

- Up One Level
  ![alt text](images/cd_movments_3.PNG)

- Up Two Level
  ![alt text](images/cd_movments_4.PNG)

---

## 5. Install two tools every senior engineer uses daily:

> sudo apt update && sudo apt install -y tree tldr bat

#### Now try,

> tree -L 2 ~

![alt text](images/tree_cmd_1.PNG)

#### practical examples instead of man pages

> tldr ls

![alt text](images/tldr_ls.PNG)

---

### Hands On

- Task 1

- > mkdir -p ~/linux-mentorship/phase1
- > cd ~/linux-mentorship/phase1
- > pwd # confirm location
- > ls -la

![alt text](images/hands_on_task1.PNG)

- Task 2 (Create First Linux Journal)

- > echo "Phase 1 Day 1 $(date)" > journal.md
- > bat journal.md

![alt text](images/bat_journal.PNG)

#### Note: Here, I faced a problem that bat was installed in my machine.

- I installed bat by using the following command.

  > sudo apt install bat

- It’s a very common Ubuntu package conflict that happens to almost everyone on Ubuntu 24.04 (which you are running).

#### Here’s exactly what happened:

- When we ran sudo apt install -y ... bat, Ubuntu installed Bacula’s BAT (a backup administration tool).
- The tool we actually wanted is the modern bat (the cat replacement with syntax highlighting by sharkdp).
- On Debian/Ubuntu, the modern bat binary is deliberately installed as batcat (not bat) to avoid conflicting with the older Bacula tool.

- That’s why bat journal.md showed the long “Usage: bat ...” help text and the copyright for Kern Sibbald (Bacula) instead of showing your journal file.

#### How that has been Debugged

![alt text](images/bat_debugged.PNG)

#### How it was fixed permenantly?

#### Added alias so `bat` always means the nice cat clone

- > echo 'alias bat="batcat"' >> ~/.bashrc
- > source ~/.bashrc

#### And then it has been tested with following command.

> bat journal.md

![alt text](images/bat_journal.PNG)

---

##### More Detail Journaling

![alt text](images/journal_md_in_details.PNG)
