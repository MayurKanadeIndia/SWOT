# Objective: manipulating data efficiently

### 1. Redirection & Pipes (The Real Power of Linux)

1. > Overwrite file `command > file.txt` ![alt text](images/file_overwrite.PNG)
2. > Append to file `command >> file.txt` ![alt text](images/file_append.PNG)
3. > Redirect only errors stderr `command 2> error.log` ![alt text](images/file_save_standard_error.PNG)
4. > For both output and errors `command &> all.log` ![alt text](images/file_save_both_error_and_log.PNG)
5. > Throw away all output commonly used in scripts. `command > /dev/null 2>&1` ![alt text](images/file_throwaway_output.PNG)

### Note: `2>&1` and `&>` are same, but they have different compatibility rules.

| Feature      | 2>&1                                                 | &>                                            |
| ------------ | ---------------------------------------------------- | --------------------------------------------- |
| What it does | Merges stream 2 into stream 1.                       | Merges both streams automatically.            |
| Syntax Style | Explicit and traditional.                            | Short and modern.                             |
| Portability  | Works in all Linux/Unix shells (sh, bash, zsh, ksh). | Works in Bash and Zsh, but fails in POSIX sh. |

### Pipes (): Pass output of one command as input to another.

1. > `ls -l | less` ![alt text](images/Pipe_1.PNG)
2. > `cat /var/log/syslog | grep "error"` ![alt text](images/Pipe_2.PNG)
3. > `px aux | grep nginx` ![alt text](images/Pipe_3.PNG)

### tee: Split output (show on screen + save to file)

1. > see output + save to file `ls -l | tee listing.txt` ![alt text](images/tee_1.PNG)
2. > append mode `ls -l | tee -a listing.txt` ![alt text](images/tee_2.PNG)

---

### Text Processing

1. > operational data saved into file. ![alt text](images/operational_data.PNG)
2. > operations with the commands. ![alt text](images/data_processing.PNG)

---

# Must-know commands

1. > copy recursively: `cp -r source dest` ![alt text](images/copy_from_src_to_dest.PNG)
2. > for move/rename: `mv oldname newname` ![alt text](images/mv_cmd.PNG)
3. > careful! (use with caution): `rm -rf dir` ![alt text](images/delete_operation.PNG)
4. > create parent dirs: `mkdir -p`
5. > create/update file: `touch`
6. > disk usage (human readable): `df -h` ![alt text](images/df_cmd.PNG)
7. > directory sizes: `du -sh *` ![alt text](images/du_cmd.PNG)
8. > memory usage: `free -h` ![alt text](images/free_cmd.PNG)
9. > `uptime` ![alt text](images/uptime_cmd.PNG)
10. > `whoami` ![alt text](images/whoami.PNG)
11. > `id` ![alt text](images/id_cmd.PNG)
