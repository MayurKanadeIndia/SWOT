# Navigate like senior engineer (this is a superpower)

- In production you will never have internet access when you need help. These are the tools we actually use:

| Command         | When to use                                  | Production Example |
| --------------- | -------------------------------------------- | ------------------ |
| command --help  | Quick one-line summary                       | ls --help          |
| man command     | Full manual (arrows to scroll, q to quit)    | man ls             |
| tldr command    | Practical examples (we installed this)       | tldr grep          |
| apropos keyword | Search all man pages for a topic             | apropos copy       |
| info command    | Alternative detailed docs (sometimes better) | info ls            |

#### Example

1. > ls --help ![alt text](images/help_to_find_info.PNG)

2. > man ls ![alt text](images/man_to_find_info.PNG)

3. > tldr ls ![alt text](images/tldr_to_find_info.PNG)

4. > apropos grep ![alt text](images/apropos_to_find_man_pages.PNG)

5. > info grep ![alt text](images/info_to_find_information.PNG)

---

### Pro tip: Add below to your aliases today for easiness.

- echo "alias h='history | tail -30'" >> ~/.bashrc
- echo "alias ?='tldr'" >> ~/.bashrc
- source ~/.bashrc

#### Now you can type ? ls or h anytime.

---

### Finding things fast (the commands you will type 100 times a week)

1. > `which` shows full path of the real binary ![alt text](images/which.PNG)
2. > `whereis` shows binary + man page + source ![alt text](images/whereis.PNG)
3. > `type` tells you if it's a built-in, alias, or binary ![alt text](images/type_cmd_1.PNG)
4. > `type -a` shows ALL versions (alias + binary) ![alt text](images/type_cmd_2.PNG)

---

### Find Command : The Swiss Army Knief for searching files.

1. > find all markdown files in home (.md files) ![alt text](images/find_cmd_1.PNG)
2. > only regular files containing "conf" ![alt text](images/find_cmd_2.PNG)
3. > files modified in last 24h ![alt text](images/find_cmd_3.PNG)
4. > files bigger than 10MB ![alt text](images/find_cmd_4.PNG)
5. > ignore permission errors (common in prod) ![alt text](images/find_cmd_5.PNG)

### grep – Search inside files (you will live in this command)

1. > basic search ![alt text](images/grep_cmd_1.PNG)
2. > recursive search in directory ![alt text](images/grep_cmd_2.PNG)
3. > case insensitive ![alt text](images/grep_cmd_3.PNG)
4. > show line numbers ![alt text](images/grep_cmd_4.PNG)
5. > multiple patterns (regex) ![alt text](images/grep_cmd_5.PNG)

### `locate` superfast filename search (but it needs database.)

1. > First run one time > sudo updatedb
2. > `locate <file_name>` ![alt text](images/locate_cmd.PNG)

### Real-world connection:

In Kubernetes nodes or Docker hosts, you will constantly do:

1. > `find /var/lib/docker -name "*.log"`
2. > `grep -r "OOMKilled" /var/log/containers/`

---

### Hands On Task

##### Task 1

1. > Update your journal.md ![alt text](images/journal_md.PNG)
2. > `tldr find` ![alt text](images/tldr_to_find_info.PNG)
3. > `man grep | head -30` ![alt text](images/man_for_grep_30_lines.PNG)
4. > `apropos search` ![alt text](images/apropos_for_search.PNG)

---

##### Task 2

1. > `cd ~/linux-mentorship/phase1`
2. > `mkdir -p search_lab/{logs,configs}` ![alt text](images/search_lab.PNG)
3. > `echo "ERROR: database connection failed" > search_lab/logs/app.log`
4. > `echo "server_name localhost;" > search_lab/configs/nginx.conf`
   > ![alt text](images/search_lab_2.PNG)

#### Task are as follows

1. > find full path of `tldr` command. ![alt text](images/whereis_for_tldr.PNG)
2. > find every file in search_lab folder that contains the word "ERROR". ![alt text](images/hands_on_task4.PNG)
3. > find all `.conf` files in the entire /etc directory. ![alt text](images/find_conf_in_etc_folder.PNG)

---

#### Troubleshooting Exercise (do this now)

1. > `grep "something" nonexistent-file.txt`
2. > You will get an error. Fix it using the commands from today (hint: 2>/dev/null or redirecting errors is a common production trick). ![alt text](images/trouble_shoot_excercise.PNG)

#### Final Task

1. > `which tldr`
2. > `find ~/linux-mentorship/phase1 -name "*.md"`
3. > `grep -r "Phase 1" ~/linux-mentorship/phase1/search_lab`
4. > `tree ~/linux-mentorship/phase1/search_lab`
5. > `bat journal.md`

> output ![alt text](images/required.PNG)

---
