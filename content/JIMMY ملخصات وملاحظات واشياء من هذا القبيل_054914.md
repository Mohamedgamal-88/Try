# RH
## **DAY1**
### **1. Basic Navigation Commands**
- **`pwd`** → _Print Working Directory_
- **`ls`** → _List directory contents_
        - `ls -l` → Long listing (permissions, owner, size, date). OR  " `ll` "   
        - `ls -a` → Shows hidden files (files starting with `.`).
        - `ls -lh` → Displays human-readable sizes (KB, MB).
- **`cd`** → _Change Directory_
	- **`cd /path/to/dir`** → Go to a specific directory.
	- **`cd ..`** → Move up one level (to parent directory).
	- **`cd .`** → Stay in the current directory (useful for certain operations like copy).
	- **`cd -`** → Go back to the previous directory.
	- **`cd ~`** → Go to the home directory.
	- If directories are at the same level:
	    - Use `cd ../folder_name` → Go to a sibling directory.
---
### **2. Root & User Management**
- **Shell prompt symbols:**
    - `#` → Root user (superuser).      
    - `$` → Regular user.
    - **`~`** →  home directory of the current user
    - **`sudo`** → Run a command as root.  
	- **`su`** → Switch user (defaults to root if no username given).
	- `su -`  → Switch to root with full environment.
	- **`exit`** → Return to the previous user or exit the shell.
	
- **Change root password:**
    ```bash
    sudo passwd root
    ```
    To change your own password :
    ```bash
	passwd
    ```
    To change the password by the root :
    ```bash
    sudo passwd 
    ```
	-اليوزر علشان يغيرها لنفسه محتاج يدخل الباس القديمة ويعمل واحدة كومبلكس ولكن الروت يقدر يدخل اي باس

---
### **3. Viewing and Writing Files**
- **`cat`** → Display file contents.
    - **Example:**    
        ```bash
        cat file.txt
        ```
- **Write to file using `redirection`:**
    - `echo "Hello" > file.txt` → Overwrites the file.
    - `echo "World" >> file.txt` → Appends to the file.
لو مفيش ملف هتنشئه و مع اي كوماند مش شرط echo 
- ممكن اقول cat > file 15  دا كدا بيعمل الفايل او بي overwrite  لو موجود و يفتحلي الملف اكتب فيه ولو قلت cat file11>>file16 دا كدا هيحط الحاجات بتاعت فايل 11 بعد فايل 16
- **Create empty file:**
    ```bash
    touch file1
    ```
	لو عايز تنشئ كذا ملف مرة واحدة ممكن تقول 	touch file{1..10}

- **Editors:**   
    - `nano` (simple)
    - `vim` (powerful, recommended for Red Hat)
    - `gedit` → GUI, beginner-friendly

[vim clean sheet ](https://devhints.io/vim)

---

### **4. File & Directory Management**

- **Create directories:**
    ```bash
    mkdir dir1
    mkdir -p dir1/dir2/dir3  # Nested directories
    ```

`/dir1` = under root, dir1 = under current user home.

- **Copy a file:**
```bash
cp file.txt /home/user/Documents/ #Copy file to directory,overwrite if there.
cp -R /source/folder /destination/ # Copy the entire folder & its contents.

```
- **Rename or move a file:**
    ```bash
    mv old.txt new.txt #Rename
    mv file.txt /home/user/Documents/  #move
    ```

- **Delete a file or directory:**
    
    ```bash
    rm file.txt
    rm -r dir1/  # Recursive (removes everything inside)
    ```

- **Hide a file:**  
    Add a dot at the beginning:  
  ```bash
    mv file.txt .file.txt
    ```
ممكن يبقي في ملفين بنفس الاسم واحد قبله دوت و دول كدا فايلين مختلفين
  
---

### **5. Command Shortcuts & History**

- **`ALT + .`** → Inserts the last argument from the previous command.
- **`!number`** →تقدر ترن اي امر اتنفذ قبل كدا عن طريق علامة التعجب و رقم الامر من الهيستوري  .   
- **`!cat`** → Runs the last command starting with `cat`.
- **Show history:**
    ```bash
    history
    ```

---
### **6. Help & Documentation**
- **`man command`** → Manual page (opens in a separate window).
- **`info command`** → Detailed info (not always available in RHEL 10).
- **`command --help`** → Quick help in the same terminal.
- **Note:** Not all commands support all three, but most do.
---
### **7. Searching for Files and directories** 

- **Find by name:**  
    ```bash
    find / -name "password"
    ```

- **Search in specific path:**
    ```bash
    find /etc -name "*.conf"
    find /etc -iname "*.conf" #case-insensitive

    ```
---

### **8. Output Redirection & Error Handling**

- **Redirect standard output and errors:**
    - `>` → Writes output to a file (overwrites).
    - `>>` → Appends output to a file.
    - `2>` → Redirects errors  to a file.
    - 2>> → Appends errors to a file
    - 2> /dev/null →  Discard errors
    - &> /dev/null → Discard both output & errors
	ممكن في نفس السطر اعمل كذا redirection مثلا ابعت الاوت لفايل و الايرور لفايل تاني
- **/dev/null:**  
- زي صندوق المهملات اي حاجة هناك بتتمسح بس مبقدرش ارجعها 


---

### **9. Pipelines & Tee**

- **Pipe (`|`):** Sends the output of one command as input to another.
    
    ```bash
    ls /etc | grep re
    ```    
- **tee:** Displays output and writes it to a file at the same time.
    ```bash
    ls | tee files.txt
    ```

---



### **10. Links**

- **Symbolic link (soft link):**
    ```bash
	ln -s /home/user/original /home/user/symlink 
    ```
    زي الشورت كت , يشير للملف الاصلي ولو الملف اتحذف هيبقي ملهوش لازمه
- **Hard link:**
    - Shares the same inode (same physical data).
    - Must be on the same partition
    - بيفضل موجود لو الملف الاصلي اتحذف فهي نسخة اخري من نفس الملف
    - **Example:**
        ```bash
	        ln file1 file2
	        ```
- Show inode :    ls  -i


---

### **11. Storage Management**
- `lsblk` lists information about block devices (disks, partitions, and virtual devices).
- It shows details like name, size, type, and mount point in a tree-like format.
---


## **DAY 2**
### **12. Variables in Bash**
- Create a variable:
    ```bash
    mypath=dir1/dir2/dir3
    ```
- Use the variable in a command:
    ```bash
    cat $mypath/file1
    ```
- Variable replaces the text, so you don’t need to type the full path every time.
- You can also store text:
    ```bash
    mystring="welcome"
    echo $mystring
    ```
- Variables are temporary (lost after closing terminal). To make it permanent, add to `~/.bashrc`:
    ```bash
    echo 'mypath=dir1/dir2/dir3' >> ~/.bashrc
    ```
    
    لازم تستخدم << مش واحدة بس والا تبقي مسحت كل اللي في الملف 
    
-  **Bash: Variables & Command Substitution**.
    ```bash
	set   # lists all shell variables
	set | grep mypath   # filters variables containing 'mypath'
	unset mypath        # deletes the variable 'mypath'
	echo "My path is $mypath"  
	echo "Today is $(date)"   # replaces $(date) with current date
	    ```
	لو ضفته في    `.bashrc` لازم تمسحه بنفسك لو هتعمله unset 

---
### **13. Aliases in Bash**
- Create alias:
    ```bash
    alias hello='echo Hello'
    ```
    Use **single** or **double quotes**.
- Example:
    ```bash
    alias pingme='ping -c 3 127.0.0.1'
    ```
	- البينج بيرن ومش بيقف عند رقم معين لو محددتش و -c 3 معناها هيبعت 3 مرات بس
- Show all aliases:
    ```bash
    alias
    ```
- Remove alias:
    ```bash
    unalias hello
    ```
- Aliases are temporary unless added to `~/.bashrc`.
- `$` works with alias too :
	```bash
	alias mycmd='ls -l'
	echo "Running: $(mycmd)"
	```
---

### **14. Linux Users**
- **Types of users**:
    - **Root (super user)** → UID = 0
    - **System users** → UID 1–999 (used for services)
    - **Regular users** → UID ≥ 1000

- 1. **Root (Super User)**   
    - الروت و يقدر يتحكم في كل حاجة 
2. **System Users**
    - Used by system processes and services, not by humans.
    - For example: `dhcp`, `nginx`, `mysql` services run under their own system user accounts for security isolation.
    - They cannot log in normally because they usually have `/sbin/nologin` or `/bin/false` as their shell.
    - Purpose: limit the impact of a compromised service (principle of least privilege).
3. **Regular Users
    - Created for human users to log in and perform normal tasks.
    - Cannot perform administrative tasks unless given `sudo` privileges.
    - Each regular user has a home directory (e.g., `/home/username`) and owns personal files. 

- User info is in:
    ```bash
    cat /etc/passwd
    ```
    Example:
    ```
    ali:x:1001:1001:Ali:/home/ali:/bin/bash
    ```
	- **ali** → Username 
	- **x** → Password placeholder (actual password in `/etc/shadow`)
	- **1001** → UID (User ID)
	- **1001** → GID (Primary group ID)
	- **Ali** → Comment/Full name (GECOS field)
	- **/home/ali** → Home directory
	- **/bin/bash** → Login shell


- Passwords (hashed, not plain text) are stored in:
    ```
    /etc/shadow
    ```

- Groups are in:
    ```
    /etc/group
    ```
- Check user ID and groups:   
    ```bash
    id ali
    ```
- **Primary group** → default for files created by the user.
- **Secondary groups** → extra groups.

---

ا
### **15. Manage Users & Groups**
- 
	```bash
	 sudo useradd ali          # creates user 'ali'
	sudo groupadd HR           # creates group 'HR' without users 
	sudo usermod -G group1,group2 ali # sets 'ali' only in 'group1' and 'group2' and remove from others groups
	sudo usermod -aG HR ali    # adds 'ali' to 'HR' without removing other groups
	sudo userdel ali           # deletes user 'ali' (home directory remains)
	sudo userdel -r ali        # deletes user 'ali' and their home directory
	sudo groupdel HR           # deletes group 'HR',you must remove users first
	sudo usermod -g HR ali     # changes primary group of 'ali' to 'HR'
    ```

- لو ضفت يوزر جديد بال useradd مش بالgui  من غير اي اضافات مش هيبقي فيه ال Home Directory زي downloads و Documents
- مينفعش احذف ال primary group  خالص ليوزر الا لو ضفته لجروب تاني يبقي فيه primary group 
- مينفعش احذف جروب الا لو مسحت اليوزرز اللي فيه
- علشان ادور هو اليوزر اتعمل ولا لا ممكن اعمل grep لاسم اليوزر في etc/passwd/
- علشان ادور علي يوزر في جروب ايه ممكن ادور عليه في etc/group/ بيبقي فيه الجروبات والاعضاء اللي فيها

- اقدر اغير اسم اليوزر

```bash
sudo usermod -l newname oldname
```

بس دا مش هيغير  اسم الـ home directory  إلا لو استخدمت `-d` مع `-m` لنقل المجلد:

```bash
sudo usermod -l newname -d /home/newname -m oldname
```
وهيفضل بنفس ال UID  برضك ولكن اقدر اغيره بس لازم اغير صلاحيات الملفات اللي عملها لانها هتبقي مربوطة بال UID القديم

---

### 2. **شروط مهمة**

- لا يمكن أن يكون المستخدم متصل حاليًا (يجب تسجيل الخروج).
    
- يجب أن لا يكون هناك عملية تعمل باسم هذا المستخدم.
    
- الاسم الجديد يجب أن يكون فريد (مش مستخدم من قبل).
    

---

### 3. **تأثيرات التغيير**

- قد تحتاج لتحديث أي ملفات إعدادات تعتمد على اسم المستخدم القديم.
    
- الـ UID يظل نفسه، فقط الاسم يتغير.
    
- الـ home folder لو نقلته مع `-d -m` سيتم تحديثه تلقائيًا.
    

---

### **16. Password Management**

- Set or change password:

    ```bash
sudo passwd ali          # sets or changes password for user 'ali'
sudo chage -d 0 ali      # sets last password change to 0 → user must change at next login , you can change anything in shadow structure
sudo chage -l ali        # displays info: last password change, expiration, warning, inactivity
sudo usermod -L ali       # locks the account (prevents login)
sudo usermod -U ali       # unlocks the account (allows login)
sudo passwd -l ali        # locks account (prepends '!' in /etc/shadow)
sudo passwd -u ali        # unlocks account (removes '!' from /etc/shadow)
    ```
**Structure of `/etc/shadow`**
```bash
sudo cat /etc/shadow  #you can use grep for faster search 
```

Use the anchored pattern when you specifically want the `ali` account’s entry.

username:password:last_change:min:max:warn:inactive:expire:reserved
- `username` → اسم اليوزر
- `password` → بيبقي هاشد تكست (or special symbol like `*` or `!` if account is locked)
- `last_change` → اخر مرة الباس اتغير  (days since 1 Jan 1970)
- `min` → اقل عدد من الايام قبل ما اليوزر يقدر يغيره تاني لو غيره
- `max` →  اقصي عدد من الايام اللي لو وصله لازم يغيره قبل ما ينتهي
- `warn` → التحذير قبل ما يوصل للعدد الاقصي من الايام
- `inactive` →  عدد الايام قبل ما الحساب يقفل اللي كان لسا شغال بعد انتهاء الباس  
- `expire` →تاريخ الانتهاء بتاع الحساب بالكامل  
- `reserved` → Reserved for future use (usually empty)
الكلام دا كله ممكن اغيره لاي يوزر من ال shadow  بس الاحسن اقول بامر chage

---
### **17. Consoles and Sessions**
-
- Switch between consoles:
    - **Ctrl + Alt + F3..F6** → TTY consoles.
    - **Ctrl + Alt + F1** → login screen.
    - **Ctrl + Alt + F2** → GUI.
- Show active sessions:
    ```bash
    w
    ```
- Exit session:
    ```bash
    exit
    ```
اقدر اخش علي الروت من ال gui  بيبقي في ال unlisted 

---

### **18. Sudo & Permissions**
- `sudo` = Super User Do.
- Wheel group = admin group for users who are allowed to use `sudo`.
اي يوزر عايزه يستخدم sudo بحطه فيها يعني دا جروب فيه صلاحيات ال sudo للاوامر كلها
- Edit sudoers:
    ```bash
    sudo vim /etc/sudoers
    ```
دا الملف الرئيسي اللي فيه صلاحيات ال sudo لكل يوزر وجروب
- Add custom sudo rule:
    ```bash
    sudo vim /etc/sudoers.d/HR-file
    ```

لو عايز مثلا اخلي جروب معين يقدر يعمل حاجات معينة بس مثلا يضيف user  ويديله pass  بال sudo
    ```
    %HR ALL=(ALL) /usr/sbin/useradd, /usr/bin/passwd
    ```
ممكن اشيل % وادي الصلاحيات ليوزر بشكل مباشر بس الاحسن احدد جروب
- Find full path of a command:
    ```bash
    which useradd
    ```

---

### **19. File Permissions**
- Check permissions:
    ```bash
    ls -l file
    ls -ld dir1 # d to show permissions of directory not files inside it
    ```
- Structure:
    ```bash
    -rw-r--r--.  1  ali  developers  1024  Aug 22 10:15  notes

    ```
	- **-rw-r--r--** → Permissions (`-` for file, then `rw-` owner, `r--` group, `r--` others)
	- No extra symbol → No extended attributes or ACLs.
	- `.` (dot) → The file has SELinux context or extended attributes.
	- `+` (plus sign) → The file has ACLs (Access Control Lists).
	- 1 → Link count (usually `1` for files)
	- ali → Owner (user)
	- developers → Group
	- 1024 → File size in bytes
	- Aug 22 10:15 → Last modification date and time
	- notes → File name

- Permission types :
    - **r** = read
    - **w** = write
    - **x** = execute
 On a FILE :
	- r (read) → اقدر اقرا محتوي الفايل.
	- w (write) → اقدر اعدل علي محتوي الفايل.
	- x (execute) →اقدر ارن الفايل يعني مثلا لة سكريبت عايز اشغله.

On a DIRECTORY :
	- r (read) → اقدر اشوف  اسماء الفايلات اللي فيه ايه  (ls dir)
	- w (write) → اقدر اضيف وامسح الفايلات اللي جواه
	- x (execute) → علشان اقدر اخش عليه اصلا و غالبا لازم تبقي شغال (cd dir)
	

- Change permissions:    
    ```bash
    chmod u+x file #u(user) g(group) o(other) a(all) (+,-,=)
    chmod 755 file
    chmod -R 755 directory #Recursive
    ```
    الارقام دي هي الباينري للrwx يعني 7 دي 421 كله موجود ال 5 دي كدا ال r-x
- Change owner:
    ```bash
    sudo chown user:group file
	sudo chown -R user:group directory #Recursive
    ```
لو عايز اغير المالك بتاع ملف 

---

### **20. ACL (Access Control Lists)**
- لو عايز اضيف جروب او شخص معين صلاحيات معينة وهو لا اليوزر ولا في الجروب بتاعه ومش عايز ادي كل الباقي نفس الصلاحيات دي 
    ```bash
    sudo setfacl -m u:ali:rw /test/file #Add ACL (u=user,g=group)(-R for dir recur)
    getfacl /test/file #View ACL
    sudo setfacl -x u:ali /test/file #Remove ACL
    sudo setfacl -b /test/file #- Remove all ACL
    ```

---

### **21. Logs**
- Security logs:
    ```bash
    sudo tail /var/log/secure
    sudo tail -f /var/log/secure  # Real-time
    ```
لو عايز اشوف اللوجز اللي حصلت واقدر اضيف -f علشان تبقي في الريل تايم ودي بتعرض محاولات التسجيل وعمليات ال su و اوامر ال sudo


---


## **DAY 3**
### **22. Processes & Jobs**
**Parent & Child Process**  
A program that opens another process creates a _child process_ using `fork()`.
Show process tree:
```bash
pstree
pstree -p    # with PIDs
```

Show running processes:
```bash
ps            # current user only
ps lx         # shows parent (PPID)
ps aux        # all users + CPU & RAM usage
```
- `a` → show processes for all users (with a terminal).
- `u` → display in a user-friendly format (with columns like USER, %CPU, %MEM, etc.).
- `x` → include processes not attached to a terminal (like background daemons).
---
### **23. Virtual Memory (Swap)**
Virtual memory (swap): Extends RAM by using disk space; Linux uses a separate partition, while Windows takes it from all partitions.

---

### **24. Background & Jobs**

- Run process in background:

```bash
firefox &
```
- Run multiple jobs:
```bash
sleep 1000 & sleep 1000 &
```
- `sleep` pauses the execution of a script or command for a specified amount of time.

- Process = any running program with a PID, managed by the OS.  
- Job = process (or group) started from a shell, tracked by that shell with a Job ID (`%`).

Check jobs:
```bash
jobs
```
	
	- `+` → current job (highest priority), this is the one that `fg`            will bring to the foreground by default.
	
	- `-` → previous job (second priority, after `+`).
	   
	- Other jobs → have no sign, so lowest priority.

Bring job to foreground:
```bash
fg       # default (+ job)
fg %2    # specific job
```
Send to background after stop:
```bash
Ctrl+Z    # stop job
bg        # resume in background
```
Stop & terminate:  
`Ctrl+C` → terminate (SIGINT)  
`Ctrl+Z` → stop (SIGSTOP)

---

### **25. Kill Processes**
The `kill` command in Linux is equivalent to “End Task” in Windows, but with multiple signals you can use, unlike Windows

Kill by PID:
```bash
kill <PID>          # default SIGTERM
kill -9 <PID>       # force (SIGKILL)
```

List all signals:
```bash
kill -l
```
The most used :
- Signal 15 (`SIGTERM`) is the default and is equivalent to “End Task.”
	- Gracefully terminates the process: children first, then the parent.   
- Signal 9 (`SIGKILL`) forcefully kills the process immediately.
- Signals 19 and 20 are for pausing a process (`SIGSTOP`, `SIGTSTP` – e.g., `Ctrl+Z`).
- Signal 18 (`SIGCONT`) resumes a stopped process.

Kill by job:
```bash
kill %2
```
	لو نسيت ال % و كتبت مثلا 1 فهو كدا مش هيتارجت الجوب انما هيشوف البروسيس اللي اي دي بتاعها واحد ودا كدا هيخلي السيتسم يكراش 
Kill by name or pattern:
```bash
killall firefox
sudo pkill -u username #processes owned by **another user**
pkill -9 -t pts/2 #processes running on the terminal pts/2
sudo kill <PID> #**single process** by PID

```
---

### **26. Process Monitoring**

Monitor processes in real-time:
sorts processes by CPU usage by default
```bash
top
```

Inside `top`:  
`q` → quit  
`?` → help  
`k` → kill process  
`W` → save config

You can kill a process from `top` by pressing **`k`** and entering its PID and signal (default`15`). For processes owned by another user, run `top` with `sudo`


Load test:
```bash
cp /dev/zero /dev/null
```
بيستهلك البروسيسر جدا لانه بيقعد يولد اصفار ويرميها فهو مش بيعمل ملف حقيقي ياخد مساحة انما انا بستهلك البروسيسر بشكل مستمر مش اكتر

---

### **27. SSH**
Connect to remote machine:
```bash
ssh username@IP
```
لو نفس اسم اليوزر في الاتنين مش محتاج اكتبه 
Show active sessions:
```bash
who     #Shows who is logged into the system
w       #Shows who is logged in and what they are doing ,shows both local and remote sessions
w -i    #to show the IP addresses of remote session
```
Kill SSH session:
```bash
sudo pkill -t pts/2
sudo pkill -9 -t pts/2   # force kill
```
 لو في اتصال ssh  مش هيتقفل الكونكشن بالطريقة الاولي ولكن هيقفل بال force kill
 - SSH Key Auth
	
	```bash
	ssh-keygen #Generate SSH key
	ssh-copy-id user@server #Copy key to server
	cat ~/.ssh/known_hosts #Check client keys
	sudo ls /etc/ssh/  #Check server keys
	sudo systemctl reload sshd #reload SSH service
	```
- ال ssh copy id علشان الكلاينت يبعت للسيرفر البابلك كي بتاعه ويسجل فيما بعد من غير الباس 
- ال known_hosts دي انا كدا كيوزر بشوف البابلك كي للاجهزة اللي دخلت عليها قبل كدا
- اللي تحت /ssh دا كدا بشوف البرايفت والبابليك كي الخاصين بيا
- في حاجة اسمها passphrase دي غير كلمة المرور دي بتستخدم عشان احمي البرايفت كي ولو سجلت بطريقة الpasswordless  لسا هيطلب مني ادخل ال passphrase

- Enable root SSH login:
	- 
		```bash
		sudo vim /etc/ssh/sshd_config.d/myroot.conf
		# Add:
		PermitRootLogin yes
		```
او ياما اعمل فايل مستقل واعمله include داخل الفايل
- **SSH Encryption Process**
	- Initial connection: asymmetric encryption    
	    - Client encrypts with server’s public key (plus user credentials, symmetric key)
	    - Server decrypts with private key
	- After connection: communication switches to symmetric encryption
	- User keys stored in:
	    - `~/.ssh/` → `id_rsa`, `id_rsa.pub`, `known_hosts`
	    - `/etc/ssh/` → public keys distributed for access
- Run command over SSH without full session:
	```bash
	ssh user@IP "command"
	```
	ممكن ارن كوماند بال ssh و بعدها اقفل الكونكشن بعدها مباشرة  
  - Use hostnames like DNS → edit:
	```bash
	/etc/hosts
	```
	اكتب جواها ال ip  والاسم اللي هدخل بيه مكانه لان مفيش علي الجهاز اصلا dns server 


	-  Passwordless Login
		First → sends user/pass + public key  ,The server stores your public key in `~/.ssh/authorized_keys`.
		Later → authenticate using private key only (no password)
		
باختصار في اول مرة بتدخل عادي اليوزر والباس و بتعمل كوبي للبابلك كي في السيرفر 
في المرات اللي بعدها السيرفر بيشفر رسالة عشوائية بالبابلك كي اللي خزنه عنده ويبعت ليك وانت هتفكه بالبرايفت كي اللي عندك وهتبعت الرسالة لو لقاها هي نفس الرسالة العشوائية يبقي كدا تمام

---

### **28. Service Management**
- **Windows:** Uses Windows Service Management. Services can be set to:
    - Automatic
    - Automatic (Delayed)        
	- Manual   
	- Disabled

- **Linux:** Services have 3 main states:
    - Enabled → Starts automatically at boot
    - Disabled → Does not start at boot
    - Static → Cannot start automatically; must be started manually

-   **Listing Services in Linux**
	```bash
		systemctl list-units --type=service --all #running, failed, inactive
		systemctl list-unit-files --type=service --all #enabled,disabled,Static
	```

-  **Check Status of a Service**
	```bash
		sudo systemctl status sshd
	```
	- `enabled` → service is set to start at boot
	- `running` → currently active
	- These are independent: a service can be enabled but not running

- **Dependencies**
	
	```bash
	systemctl list-dependencies sshd
	```
	- **Green** → Required dependencies
	- **Gray** → Optional dependencies

- **Start, Stop, Reload, Restart**
	
	```bash
	sudo systemctl start ssh
	sudo systemctl stop ssh
	sudo systemctl restart ssh   # stops and starts, changes PID
	sudo systemctl reload ssh    # keeps PID, not all services support reload
	sudo systemctl try-reload-or-restart ssh
	```
	- `enable --now` → enable + start immediately   
	- `disable --now` → disable + stop immediately
	
لو فتحت سيشن ssh  وقفلت بعدها ال service وقلت stop هتفضل شغالة عادي ولكن لو قفلت السيشن  ثم بعد كدا جربت اشغلها مش هقدر



- **Masking a Service:**
	
	```bash
	sudo systemctl mask sshd   # prevents even root from starting it
	sudo systemctl unmask sshd # allows it to start again
	```
	- Masking: Links the service unit to `/dev/null`, making it unstartable.

 
 - **Daemon vs Service  :**
	Daemon  :A background process that runs continuously, providing services, and may or may not be managed by systemd.  
	Examples: `sshd`, `httpd`, `cron`
	
	Service :A systemd unit that manages a daemon or task, providing control over its start, stop, and monitoring using `systemctl`.  
	Examples: `ssh.service`, `apache2.service`


- **TCP Connections**
	
	```bash
	netstat -tcp -a      # shows TCP connections
	netstat -tcp -an     # shows numeric addresses
	```
	
	- `LISTEN` → waiting for connections
	- `ESTABLISHED` → active connections


---


### **29. Network**

Show IP address:

```bash
ip -br address
ifconfig
```

Check connections:

```bash
netstat -tcp -a
netstat -tcp -an    # numeric mode
```

`LISTEN` = waiting  
`ESTABLISHED` = active

---

### **30. Logs**

Check security logs:
```bash
sudo tail /var/log/secure # Show the last 10 lines of the secure log file (security/ authentication events)

grep sshd /var/log/secure # Filter the secure log to show only SSH daemon (sshd) related entries
```
- common log files :
	- **`/var/log/secure`** (on RHEL/CentOS/Fedora) → security/authentication logs.
	- **`/var/log/auth.log`** (on Debian/Ubuntu) → similar purpose
	- **`/var/log/messages`** → general system messages (kernel + services).
	- **`/var/log/faillog`** → failed login attempts.
	- **`/var/log/lastlog`** → last login info of all users
---

### **31. Hostname**

Change hostname:

```bash
sudo hostnamectl set-hostname redhat1
```

---


## **DAY 4** 

### **32. SFTP (SSH File Transfer Protocol)**

- SFTP is FTP over SSH, used for secure file transfer on port 22.
    
- Start SFTP like SSH:
    
    ```bash
    sftp username@ipaddr
    ```
    
- **Show all commands:** type `?` in the prompt.
    
- **Important commands:**
    - `get` → download file from server (can specify full path)
    - `put` → upload file to server (use `-R` for directories recursively)
- If a command fails, specify the full path (e.g., `e:\path\file`).
    
- To execute commands on the local machine without leaving SFTP, use `l` (local), e.g.:
    - `lls` → lists local files
    - `ls` → lists server files        
- **Note:** SFTP only transfers files; to execute more commands on the server, use **SSH**.


---

### **33. Network Device & Connection**

- **Device:** Physical network card.
- **Connection:** Configuration assigned to the device.
- One device can have **multiple connections**.

**Useful commands:**

```bash
sudo nmcli device status       # list devices (ens160 = PCI slot number)
sudo nmcli connection show     # list connections and type (static, DHCP)
```

- **Add new connection:**
```bash
sudo nmcli connection add con-name ens224-DHCP type ethernet ifname ens224 ipv4.method auto autoconnect yes
```
	- ifname must match the device name.
	- autoconnect yes →Enable automatic connection on boot
	- auto → gets IP via DHCP.

- **Activate/deactivate connection:**  
	```bash
	sudo nmcli connection up <name>
	sudo nmcli connection down <name>
	```
- **Modify connection:**
	    - `+` → add setting
	    - `-` → remove setting
	    - no symbol → replace setting
- Can disconnect the device temporarily.
	```bash
	# Disable the network interface (disconnect)
	sudo ip link set $INTERFACE down
	# Enable the network interface (reconnect)
	sudo ip link set $INTERFACE up
	```

- **Check IP routes & metric:**
	```bash
	ip addr                 # ip , mac info
	ip route                #Gateway
	cat /etc/resolv.conf    # DNS
	sudo nmcli device show  # all in one command
	ipconfig/all            #Windows command to show all in one 
	```

- **Static connection example:**
	```bash
	sudo nmcli connection add con-name ens224-static type ethernet ifname ens224 ipv4.method manual ipv4.addresses 10.0.0.100/8 ipv4.gateway 10.0.0.1 ipv4.dns 8.8.8.8 autoconnect yes
	```

- You can also edit `/etc/NetworkManager/system-connections/` files directly. and After changes:
	```bash
	nmcli con reload
	nmcli con up <name>
	```

- **TUI interface (text-based GUI):**
	tool for managing network connections using NetworkManager.
	```bash
	sudo nmtui
	```

---

### **34. Network Diagnostic Tools**

- `tracepath` → alternative to traceroute
- `nslookup`, `host`, `dig` → get IP addresses of domains, including IPv6
- `netstat -tunap` / `sudo ss -tnuap` → show all active connections, ports, and processes
---

### **35. Package Management**

- **RPM commands:**
```bash
sudo rpm -i package.rpm       # install
sudo rpm -e package           # remove
sudo rpm -ivh package.rpm     # install with progress(####)
sudo rpm -qa                  # list installed packages
sudo rpm -ql firefox          # list files of package
sudo rpm -qc firefox          # list config files
```
 بسطب الباكج بشكل منفرد فلو معتمدة علي حاجات تانية مش متسطبة مش هتشتغل معايا
 
- **YUM / DNF:**
    بسطب الباكج وكل اللي معتمدة عليه علشان تشتغل
```bash
sudo dnf install <app>       # installs dependencies automatically
sudo dnf groupinstall "Security Tools"
sudo dnf repolist all         # list all repos
sudo dnf makecache            # refresh cache
sudo dnf grouplist            # list groups
```

لو كتبت yum  فهو مجرد alias  لل dnf  في نسخ الريد هات الحديثة 
- **Local repo setup (Red Hat):**
- الريد هات بتطلب اشتراك علشان احمل ال repos الرسمية علشان كدا بلجا للطريقة دي بعمل لوكال ريبو وبضيف  ال BassOS وال APPStream
    - Create `.repo` files in `/etc/yum.repos.d/`

- **Example AppStream Repo**
```ini
[AppStream]
name=AppStream
baseurl=file:///run/media/RHEL-10-0-BaseOS-x86_64/AppStream
enabled=1
gpgcheck=0
```
ممكن بدل الفايل احط http و ال gpgcheck حطه ب1 علشان الريد هات يتاكد هل هي سليمة وجايه من المصدر الاصلي ولا لا
-  **Copy CD Content Locally**
```bash
sudo cp -r /run/media/USER/RHEL-10-0-BaseOS-x86_64 /mypackage
```
لو عايز انسخ محتوي الiso  في مكان عندي واحطه في الريبو 
 
### **36. Web Server Setup (Apache / HTTPD)**

استخدام اللينكس كويب سيرفر شائع جدا لان اغلب المالويرز بتبقي تستهدف الويندوز
في نوعين من الابلكشين المشهورة apecha   او ngrx
**Five Steps:**
1. Install Apache:
```bash
sudo dnf install httpd
```

2. Default web page located at `/var/www/html/index.html`
```bash
sudo vim /var/www/html/index.html
```
دي الصفحة الرئيسية وباقي الملفات تحت html/ 

3. Set permissions: folders → read & execute, files → read

4. Configure firewall:
الفايروول  اسمه net filter  
```bash
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
sudo firewall-cmd --list-all #Shows the current configuration 
```

5. Enable and start service:
```bash
sudo systemctl enable --now httpd.service
sudo systemctl status httpd.service
sudo tail -f /var/log/httpd/access_log
```
بعدها اخد ال اي بي  واجربه علي اي متصفح هيشتغل
- **HTTP response codes:**
    - 1xx → Information
    - 2xx → Success (200 = OK)
    - 3xx → Redirect
    - 4xx → Client error
    - 5xx → Server error

---

### **37. SSH Access by Name (Windows Example)**

لو عايز اعمل موضوع انك تخش بالاسم بدل الip  بال ssh  علي الويندوز زي ما عملنا في اللينكس

- Edit hosts file: `C:\Windows\System32\drivers\etc\hosts`
  
- Use Notepad or append via command:

```cmd
echo "192.168.1.10 myserver" >> hosts
```

---

### **38. Mounting Storage**

```bash
sudo mkdir /mycd # Create a mount point (directory) where the CD/DVD will be mounted

sudo umount /dev/sr0 # Unmount the device if it is already mounted to avoid conflicts

sudo mount /dev/sr0 /mycd/ # Mount the device /dev/sr0 (CD/DVD drive) to the /mycd directory

```
---

### **39. File Search**
- `locate <file>` → searches database (requires `updatedb`)
- `find <path> -name <file>` → searches filesystem
- `which <command>` / `whereis <command>` → find command path
---

### **40. Web-based Server Management (Red Hat)**

- Enable Cockpit (web console):
```bash
sudo systemctl enable --now cockpit.socket
```
- Access via browser: `https://<IP>:9090` → Advanced → unsafe → login  
- Provides terminal access and server management via browser

---




# Network 
## **DAY1(5)**

### **1. Networking Overview**

- **Network Types:**
	- **LAN**(Local Area Network) : تربط الاجهزة في نطاق محدود مبني مثلا والسرعة فيها عالية 
	-  **MAN**(Metropolitan Area Network) : تربط كذا لان ببعض علي نطاق اوسع مدينة مثلا
	-  **WAN**(Wide Area Network) : النطاق الاكبر يعني تربط الشبكات بين المدن والدول عالميا
	- في الWANوال MAN يتم الاتصال من خلال مزود الخدمة (ISP).


- **Connectivity Technologies (تقنيات الاتصال):**
	- **ADSL (Asymmetric DSL):**
	سرعة التنزيل تختلف عن الرفع,التنزيل اعلي وال DSL علشان بتستخدم خطوط التليفون
	- **SDSL (Symmetric DSL):** 
	سرعة التنزيل والرفع متساوية دا لو في شركات بتبقي انسب
	- **VDSL / VHDSL:**
	إصدارات أسرع من DSL و الاسرع هي VHDSL
	- **Customer Solutions:** 
	اتصال عبر Satellite، Mobile Network، Cable TV(برضك مع النفط او السفن),Fax Modem.
	- **Dedicated Leased Line:** 
	خط مخصص للشركة فقط، بدون مشاركة الBandwidth مع حد.
	- **Ethernet WAN:** 
	بيحول الايثرنت اللي في ال LAN يشتغل علي مسافات بعيدة في شبكة WAN

	ال **PSTN (Public Switched Telephone Network):**  هي شبكة التليفونات في مصر مثلا تديرها وي 

---

### **2.Network Protocols**
**Network Protocols :هي قواعد بتنظم عملية التواصل .** 
- **Reference Models**
	- **OSI:** نموذج توضيحي لكل مرحلة .
	- **TCP/IP:** النموذج الفعلي المستخدم.

- **OSI Model Layers and Functions:**
	- **7.Application Layer**
		الواجهة اللي بيتعمل معاها المستخدم زي مثلا المتصفح او الايميل و التطبيق نفسه بيستخدم  بروتوكولات علشان تعمل المطلوب زي HTTPS,SMP,IMAP

	- **6.Presentation Layer**
		المهام بتاعتها هي التنسيق (Formatting) والتشفير (Encryption) و الضغط (Compression) 
	
	- **5.Session Layer**
		بيدير ال sessions يعني بيتاكد ان الاتصال بدا هل لسا شغال ولا لا ازي هيتقفل ولو في كذا حاجة شغالة يتاكد ان كل session شغال لوحده
		التلاته لاير اللي فوق بيبقي موجودين في الابليكشن نفسه. 
	
	- **4.Transport Layer**
		بتعمل End-to-End Communication يعني انقل البيانات من تطبيق في جهازي لتطبيق في الجهاز التاني و بتعملSegmentation انها تقسم البيانات لاجزاء صغيرة وبتعمل Multiplexing وهي انها تدي ارقام بورتات علشان تعرف اللي وصلها دا لانهي تطبيق
		في نوعين 
		- **TCP (Transmission Control Protocol)**:
		    -و ديReliable وفيها Error Correctionو  Flow Control (window size) و Connection-Oriented

		- **UDP (User Datagram Protocol)**:
			-ودي العكس في كل حاجة Connectionless بس ميزتها انها سريعة فمناسبة
			للreal time  زي الالعاب و ال VOIP

		دا كله اللي مسئول عنه ال OS نفسه مش الابليكشن 

	- **3.Network Layer**
		-بتبقي فيها  Logical Addressing اللي هو ال IP اللي  ممكن يتغير عادي و ال Routing
		-الحاجات دي بتحصل في ال OS و كارت الشبكة NIC (Network Interface Card) 

	-  **2.Data Link Layer**
		- مسئولة عن ال (MAC) physical addressing وبتبقي hop to hop 
		- - Frame components: بتضيف فريمين 
			- **Header**: Source & destination MAC addresses.
		    - **Trailer**: CRC for error checking. 
		- الحاجات دي بتحصل في كارت الشبكة في جهازك

	- **1.Physical Layer**
		-بتحول لبيتات فهي بتتحكم في مستوي الجهد والسرعة
		-مسئولية كارت الشبكة ثم بتتحول في الفزيكيال ميديا نفسها 
		-ال Carrier Protocol هو القواعد اللي بتحدد الوسيط اللي هيشيل البيانات دي علي الكابل النحاس مثلا او الفايبر او الوايرلس يبقي شغال ازي في الميديم اللي بينقل من خلاله

	اليبانات بتتقسم في كذا لاير يعني في لاير Transport بيحصل Segmentation وفي لاير ال Network بيحصل Fragmentation وممكن يحصل تقسيم تاني دا كله  علشان ال MTU (Maximum Transmission Unit) وهي اقصي حاجة ممكن تعدي مرة واحدة في الميديم نفسه

- **Encapsulation / De-encapsulation:**
	 لما بتبتعت رسالة كل لاير بتضيف Header خاص بيها (Encapsulation) و  اللي هيستقبل بيعمل العكس كلا لاير بتفهم الرسالة وتشيل الهيدر اللي في اللاير دي و تسلمه للي فوقها (De-encapsulation)
	 في الطريق عادي ممكن يحصل بشكل مؤقت (De-encapsulation) لحد لاير معين مثلا الرواتر علشان يعرف ال IP بيفك لحد لاير النيتورك ثم بيعمل ال Encapsulation وبيحط هيدر جديد لل data link layer لانه hop to hop 

   

---

### **3.Application Protocols**
- **SMTP (Simple Mail Transfer Protocol):** 
	ببعت من خلاله رسائل البريد الالكتروني
- **POP3  :** 
	بستلم من خلاله رسائل البريد وبيحذفها من السيرفر بعدها فمش هقدر افتحها من جهاز تاني
- **IMAP (Internet Message Access Protocol):**
	بستلم من خلاله رسائل البريد ولكنه بيفضل سايب نسخة علي السيرفر
    
- **FTP (File Transfer Protocol), FTPS ,SFTP :****
    كلهم لنقل الملفات الFTP غير مشفر ال FTPS بيشفرها ب SSL ال SFTP بيستخدم ال SSHفبتبقي متشفرة و ال SFTP هي الافضل في الاغلب لانها ابسط مش محتاجةSSL Certificates

- **REST API:** 
	إرسال البيانات بين التطبيقات والسيرفر عن طريقAPI .


---

### **4. Transport Layer & Ports**

- **TCP Header**
	![[Pasted image 20250829154119.png]]
		![[Pasted image 20250829154348.png]]
- **UDP Header**
	![[Pasted image 20250829154451.png]]
	![[Pasted image 20250829154509.png]]

- **DNS over UDP and TCP:**
	 UDP: في الاستعلامات البسيطة من العميل للسيرفر (أسرع وأخف).
	 TCP: لو السيرفرات بتتبادل بيانات كبيرة

- **Port Numbers (16-bit):**    
    - Well-Known: 0–1023 
	    محجوزة للبروتوكولات المشهورة
    - Registered: 1024–49151 
	    بورتات بتسجلها ال IANA لشركات او تطبيقات معينة او بروتوكولات جديدة (8080 http alternative)
    - Dynamic/Private: 49152–65535 
	    بيتخصص اوتوماتيك اثناء الاتصال من نظام التشغيل بشكل عشوائي 
	![[Pasted image 20250829155817.png]]

- **Netstat:**  
	بيعرض السيشنات المفتوحة و البورتات المستخدمة و البروتوكولات اللي شغالة

-  الVoIP بيستخدم RTP (Real-Time Transport Protocol) مع الUDP بحيث يرتب الباكيت لما تجيله ولو في باكيت وقعت ممكن يعمل simulate ليها بناءا علي الباكيت اللي قبلها  او يتخطاها .

---

### **5. IP Layer – Encapsulation / Routing**

- Routing Protocol vs Routed Protocol.
    
- IP ثابت إلا عند NAT.
    
- Connectionless (IP) → hop-to-hop.
    
- Connection-Oriented (TCP) → end-to-end.
    
- **IP Header:** يجب معرفة جميع أجزائه.
    
- Segment vs Fragmentation → يعتمد على MTU.
    
- **TTL:** منع Loops، يستخدم في Traceroute، يمكن للمهاجمين معرفة topology.
    

---

### **6. IPv4 / IPv6 Addressing**

**IPv4 Classes:**

- **A (1-126):** 2^24-2 Hosts
    
- **B (128-191):** 2^16-2 Hosts
    
- **C (192-223):** 2^8-2 Hosts
    
- **D (224-239):** Multicast (IGMP).
    
- **E (240-255):** Experimental.
    

**Subnetting / VLSM:**

- هدف: تجنب هدر الـ Hosts.
    
- حساب: 2^n → عدد الشبكات الجديدة، 2^h-2 → عدد Hosts لكل شبكة.
    

**Broadcast Types:**

- Directed vs Local.
    
- Loopback Address → اختبار السيرفر.
    
- Link-Local → fallback IP، non-routable.
    

**IPv6:**

- 4 مجموعات من 4 hex (16 bits لكل مجموعة).
    
- Leading zeros يمكن حذفها، Double Colon (::) للتقليل من الأصفار المتتالية.
    
- نطاقات: Unique Local (داخل المنظمة)، Link Local.
    
- Unspecified Address 0:0:0:0 → DHCP Server request.
    
- DHCP Spoofing → استهلاك Pool IPs.
    

---

### **7. MAC Addresses / ARP / ICMP**

- MAC: أول 6 digits للشركة المصنعة، Dash أو Colon.
    
- Ethernet: Header + Trailer.
    
- **SFD:** بداية الإطار.
    
- Broadcast MAC: FFFF.FFFF.FFFF
    
- Multicast MAC: 01:00:5E + IP multicast.
    
- ARP → IPv4 & IPv6 (NDP).
    
- ICMP → لا يستخدم Port، يستخدم Type + Code.



## **DAY2(6)**

### **1. (Switches)**

 السويتش جهاز لاير 2 و لو كان Multi-Layer هيشتغل في لاير 3 كمان .
 يقدر يقرا بعض المعلومات من الطبقات الاعلي علشان ينفذها زي مثلا لو في SSH عايز اعملها  علي السويتش او DHCP snooping فالسويتش يقدر يقرا رسائل ال DHCP علشان يقدر يطبقها

-  **(Forwarding Modes):** 
	1. **Cut-Through:**
	    - **Fast Forward:** 
		يرسل الفريم اللي بيجيله علطول من غير ما يتحقق من الsize  وال CRC
		- **Fragment-Free:**
		بيتاكد من حجم الفريم بس قبل ما يبعته
	2. **Store-and-Forward:** 
		بيتاكد من حجم الفريم وبيتاكد من ان حساب الـ CRC زي ما هو صح

	ال CRC دا لل error-detection للتاكد من ال integrity 
	الModes اللي فوق غالبا اللي بيحددها المصنع نفسه  و الاغلب بيبقي store and forward 

- **(Learning Operation):**
	
	- في الاول خالص السويتش مش بيبقي عند ال mac address table فبيتعلم من الفريمات اللي بتجيله عن طريق انه بيعمل flooding  لكل اللي متوصل بيه واللي يجيله رد يبقي هو دا الجهاز الصح و يقعد كدا يبني ال mac address table   
	![[Pasted image 20250828062829.png]]

	- وبعد كدا في ال forwarding بيعتمد علي ال destination mac address  متوصل ببورت ايه وبيبقي فيه اجهزة من سويتشات تانية لو كانت في نفس الvlan وتواصلت مع بعض
	- السويتش بيعمل reset لل Aging Time لما يجيله رسالة علشان يفضل سايب ال mac  بتاع الأجهزة دي في الجدول بتاعه

- **(Flooding):**
	-   السويتش بيعمله في حالات الـ
	- Unknown Unicast : سواء علشان لسا معملش الجدول الخاص بالماك او جاله عنوان غريب فيما بعد مش موجود عنده
	- Multicast 
	- Broadcast
	-  الفرق بين مصطلح Flooding و Broadcast:
	- Flooding: 
	- دي الالية نفسها ويتم الإرسال بنفس  mac destination address اللي جاله.
	- Broadcast: 
	- دي نوع وبتبقي مقصودة اني ابعت علي FF (Broadcast MAC Address).

-  **ARP (Address Resolution Protocol):**

	-ARP Request: 
	علشان تعرف عنوان MAC الخاص بعنوان IP معين
	
	لو  انا برسل حاجة ل IP خارج الشبكة بتاعتي  الراوتر هو اللي بيرد على طلب الـ ARP وبيحط عنوان MAC GATEWAY بتاعه في جدول الجهاز اللي طلب
	الرواتر اللي هيستقبل مني بعد كدا هيجيله source mac: r1  و ال destination mac :r2 
	والجهاز اللي كنت عايز اوصله في الاصل  هيوصله source mac:r2 اللي في شبكته و destination mac : الجهاز نفسه ولو مش عارفه الراوتر هو اللي هيطلب ARP request 

	دا كله علشان ال MAC address  بيبقي hop to hop 
---
### **2. (VLANs)** 

-بقسم ال Physical LAN لمجموعة من (Virtual LANs).
- الفرق بين Subnet و VLAN؟ 
	- مفيش فرق بين الاتنين في اللي عايزين يعملوه يعني نفس الحاجة في الاتنين هدفهم يقللوا الشبكة الكبيرة لاصغر ويعزلوهم عن بعض فالاتنين بيشتغلوا مع بعض لكل subnet بحطه في vlanمختلف . ليه بستخدم ال vlan ؟ بحيث في السويتش الواحد اقدر احط كذا subnet مختلف علشان لو عملت برودكاست تروح للvlan  اللي هو فيه بس علي عكس لو مفيش vlan كان هيبعت لكله. فال vlan عملية تنظيمية لل subnet حتي لو في اماكن بعيدة عن بعض .
	
	- الsubnet لاير3 بيقسم ال ip  لشبكات مختلفة و ال vlan لاير 2 بيقسم علي نفس السويتش 

- **Types of VLANs:****
	1. Default VLAN: 
		الـ VLAN الافتراضية العادية موجودة بشكل تلقائي وكل بورتات السويتش فيها في الاول , بتبقي للترافيك للي طالع من السويتش نفسه زي BPDU (STP) او VTP وبتبقي untagged

	2. Management VLAN:
		تستخدم لإدارة السويتشات (Configuration).

	3. Data VLAN: 
		لبيانات المستخدمين العاديين ودا بعمله بنفسي علشان لو خليتهم في ال default  اي جهاز جديد يخش هيبقي في نفس ال vlan معاهم

	4. Voice VLAN:
		لضمان (QoS) للمكالمات الصوتية.
	    بيشتغل عن طريق ان الهاتف بيبقي بين الـ PC و السويتش، ويتم إرسال البيانات بـ Tagged، بينما بيانات الـ PC تكون Untagged والسويتش بيفرق بينهم من خلال كدا

-  **Port Modes :**
	- ال access port  بيبقي بين endpoint device  و السويتش بيكون عضو في vlan واحدة 
	- ال trunk port  بيبقي رابط بين اكتر من vlan  ببعض وبيستخدم الtagging  علشان يحدد الفريم تابع لاي vlan وبيبقي بين السويتش وسويتش او راوتر او اي وجهاز بيدعم tagging

	- الـ DTP (Dynamic Trunking Protocol): بروتوكول للسويتشات لتحديد وضع البورت يبقي trunk ولا access وانواعه
	- Dynamic Auto:
	- الوضع الافتراضي، يعني البورت يقدر يبقي Trunk لو تفاوض معه سويتش تاني علي كدا ولكن لو اتوصل بجهاز البورت بتاعه access زي endpoint device  او dynamic auto هيبقي access عادي
	- Dynamic Desirable: 
	- معناه ان السويتش عايز البورت يبقي  Trunk الا لو اتوصل بجهاز فيه بورت access 
	![[Pasted image 20250828100007.png]]
	
	- مشكلة الDynamic وانه الوضع الافتراضي ان ممكن اتاكر يستغل الموضع ويطلب انه يبقي trunk فبقي شايف كل الـ VLANs.
	- الحاجات اللي مفروض تتعمل انك تحدد بنفسك جميع البورتات Trunk أو Access، وتلغي ال Negotiation والاحسن كمان يتم غلق أي بورت غير مستخدم.

-  **Inter-VLAN Routing:**
	علشان اقدر اخلي الاجهزة من vlans مختلفة تكلم بعض لان كل واحدة معزولة عن التانية فعلشان كدا لازم يتواصلوا من من خلال الراوتر
	- Types :
		-  (Legacy): 
		 كل VLAN محتاجه بورت في الراوتر علشان تبقي الGateway اللي هتخرج منه.
		
		- Router-on-a-Stick:
			هو بورت واحد وبنعمل Sub-interfaces لكل VLAN، وكل Sub-interface يأخذ عنوان IP خاص بال VLAN اللي هو فيه
		    
		- Layer 3 Switch: 
			السويتش نفسه يعمل مهمة الراوتر ويعمل Switched Virtual Interface 
	
	- لو في راوتر متوصل بسويتشين وكل سويتش فيه كذا vlan لو في اجهزة نفس الvlan متوصلة بالسويتش التاني هتقدر تكلمها عادي في الاول هتعمل flood للاجهزة اللي في الvlan دي علشان مش موجودة في ال mac table بتاعها وبعد كدا تكلمها عادي , و ال flood دا هيحصل في الvlan اللي هما مشتركين فيه بس


- **`interface vlan X`** → Creates a VLAN interface.
- **`encapsulation dot1Q X`** → Specifies the actual VLAN number on the sub-interface.
- **Note:** The interface name is just a label; dot1Q determines the real VLAN tagging


---

### **3. (STP - Spanning Tree Protocol)**

بيمنع حدوث لوب في الشبكة لو ال topology فيها اكتر من طريق بين السويتشات لانه ممكن كدا يا يخلي الفريم يوصل اكتر من مرة يا broadcast storm  وبشكل عام ال mac address table مش مستقر

-  **How does it work **
	يتم اختيار الـ Root Bridge بناءً على أقل فال Bridge ID اللي هو (Bridge Priority +MAC Address )بيقارن في الاول Bridge Priority لو تساوت يقارن ال MAC Address .
    بس انك تسيب ال MAC Address الاقل دا ليه عيب وهو انه دا الجهاز الاقدم اللي موجود عندي علشان كدا الاحسن تحديد Bridge Priority يدويا
	
	كل بورتات الروت بعد كدا بتبقي Designated وكل سويتش تاني بيختار بورت واحد يبقي Root Port (افضل بورت هيودي للروت)  باقي البورتات بين السويتشات التانية وبعضها واحدة تبقي Forwarding والتانية Blocking  ودا كله بيحصل عن طريق بيتبادلوا ال BDPU

-  **Types of STP:**
	
	1. **Spanning Tree (STP):**
	    - بياخد وقت كبير  (50 ثانية).
	    - يعمل على جميع الـ VLANs والـ Topology بأكملها.
	    - بعض الروابط خلاص هتفضل مش مستخدمة علطول .
	
	2. **Rapid Spanning Tree (RSTP):**
	    - وقت أقل (15 ثانية).
	    - نفس المشاكل التانية لسا موجودة.
	    
	3. **Per-VLAN Spanning Tree (PVST):**
	    - كل VLAN لها Root Bridge خاص بيها.
	    - فيه لينك ممكن يكون شغالForwarding في vlan ومقفول في vlan تاني .
	    - بس عيبها انها تطلب حسابات كثيرة لأن كل VLAN تحسب الروت.
	    
	4. **Rapid Per-VLAN Spanning Tree (Rapid PVST):**
	    - نفس PVST ولكن بوقت أقل.
	    - بس عيبها انها تطلب حسابات كثيرة لأن كل VLAN تحسب الروت.

	
	5. **Multiple Spanning Tree (MST):**
	    - بتقسم الـ VLANs إلى مجموعات (Instances)، فمش كل VLAN محتاجه تحسب دا كله هو كذا VLAN بقت Instance واحدة .
        
	في حالة ال PVST, Rapid PVST, MST بيتكتب الـVLAN ID من بيتات الPriority في الـBridge ID.


---

### **4. (Routing Concepts)**

- اختيار أفضل مسار (Best Path) للوصول إلى الوجهة

- **Types of Networks in a Router:**
	- **Directly Connected:** 
	- الشبكات اللي متوصلة بشكل مباشرة بالراوتر هتبقي موجودة بشكل تلقائي في ال routing table مجرد ما اعمل no shutdown للراوتر.

	- **Remote:** 
	- الشبكات اللي مش متوصله علي الراوتر ومحتاجة Routing protocol علشان اوصلها  .

-  **Routing types:**
	
	- 1.**Static Routing**
		بقول بنفسي الطريق اللي الراوتر يروحه علشان يروح للشبكة دي وفي طريقتين اني اقله
		- **Next Hop IP:** 
			انه بيحصل تاخير علشان بيبص في ال routing table علي انه يخرج الباكيت دي علي اي interface كل مرة
		- **Exit Interface:**
			عيبه انه مش واضح يعني مثلا لو ال interface دا  في سويتش متوصل عليه شبكات مختلفة فهو مش هيعرف يروح فين بعدها
	
		الاحسن فيهم هو ال  Next Hop IP والاحسن من كدا اني اقله الاتنين مع بعض 

		- ممكن اضيف اتنين Static Route يعني اخلي في Backup Route باني اديله Metric أعلى من علشان ميمسحش  المسار الاصلي .
		 - **Summary Static Route:**
			ينفع تكتب كذا شبكة في route واحد بس ولكن لازم تكون متتالية وهتروح نفس ال next hop ودا علشان مقعدش اكتب جدول كبير ودا من خلال اشوف البيتات المشتركة بينهم فانت بتجمعهم في شبكة اكبر بدل ما تكتب الشبكات الصغيرة


	**2.Dynamic Routing Protocols :** 
	- **RIP (Routing Information Protocol):**
		بيشتغل بال Distance Vector  كل راوتر بيبعت جدول ال routing table بالكامل للي حواليه بعدين يختار افضل مسار علي حسب اقل عدد hop 

	- **OSPF (Open Shortest Path First):**
	    بيشتغل بال Link state كل راوتر يرسل تحديث Link State بشكل دوري لكل اللي حواليه مش بيبعت الجدول بالكامل و كل راوتر يبني قاعدة بيانات للشبكة كلها ويحسب افضل مسار .

	وفي برضك EIGRP ودا Hybrid(Link-state ,Distance vector ) وفي ال BGP ودا Exterior Gateway Protocols اللي هي مثلا بين مزودي الانترنت او بين المؤسسات الكبيرة 

 -  **Routing Decision** 
	- **Longest bit Match:**
		الراوتر بيختار المسار اللي يتطابق مع أكبر عدد من البتات في ال IP من الrouting table
	- **Administrative Distance :**
		لو في كذا مسار ببروتوكولات مختلفة بيختار الاقل AD
	- **Metric :**
		لو في كذا مسار بنفس البروتوكول بيختار الاقل metric(حسب نوع البروتوكول)
	- **Default Route:** 
		لو ملقاش مسار للip هيخرجه علي ال default 
	- **Drop:** 
	    لو ملقاش معمول default  هيوقع الباكيت
	 اي شبكة في الانترنت انا مش هكتبلها مسار بنفسي انا بوديها لمزود الخدمة علي ال default route وهو اللي هيوصلها 
 - **Redistribution:**
	ممكن لراوترين كل واحد شغال ببروتوكول مختلف يتواصلوا باستخدام  الـ Redistribution بس لازم يكون واحد فيهم شغال علي اكتر من بروتوكول في نفس الوقت منهم اللي التاني بيستخدمه او يبقي في راوتر بينهم شغال علي الاتنين بروتوكول اللي الاتنين بيتواصلوا بيه .    


---

### **5. DHCP (Dynamic Host Configuration Protocol)**
علشان اوزع ال IPs بشكل تلقائي للاجهزة في الشبكة
 **Steps of DORA:**
1. **Discover:**
	يرسل الجهاز طلب برودكاست
	 (Source IP: 0.0.0.0، Destination IP: 255.255.255.255، MAC: FF:FF:FF:FF:FF:FF) 67 (DHCP).
2. **Offer:**
	بيبعت  سيرفر ال DHCP عرض بعنوان IP ( Unicast أو Broadcast لو ميعرفش ال MAC بتاعه).
3. **Request:**
	يطلب الجهاز واحد مالIPs اللي جتله ويبعتBroadcastعلشان يعرف كل السيرفرات انه قبل واحد.
4. **ACK (Acknowledgement):**
	سيرفر  DHCP بياكد انه حجزله ال IP .

- **هل في حاجة الجهاز بيختار علي اساسها عنوان IP لو جاله كذا واحد ؟**
	في الغالب بيختار أسرع عرض جاله  ثم فيما بعد لما بيطلب تاني بيدي الأولوية للعنوان اللي اختاره قبل كدا .


-  **IP Helper:**
	طلب الIP بيكون برودكاست و في الاغلب السيرفر بتاع ال DHCP بيبقي برا الشبكة فمش هتعرف توصله طلب البرودكاست اللي عملته علشان كدا الراوتر بيستقبل الطلب من الجهاز ويضيف ال interface اللي استقبل عليه الطب ويوديه لل DHCP سيرفر ويبعتله الرد تاني . 

-  **DHCPv6 (For IPv6):**
	 يستخدم بروتوكول ICMPv6 وفيه كذا نوع لتوزيع الـ IPv6:    
    1. **SLAAC (Stateless Address Autoconfiguration):** 
	    الراوتر بيحدد ال prefix  والجهاز هو اللي بيكون الIPمن عنده و السيرفر غير ضروري 
    2. **Stateless DHCPv6:** 
	    الراوتر بيحدد ال  Prefix , Prefix length, Default Gateway والجهاز بيكون ال IP وال DHCP سيرفر بيديه معلومات اضافية زي ال DNS  .    
    3. **Stateful DHCPv6:** 
	    شبه ال DHCP العادي يوفر كل المعلومات(IP,DG,DNS) من خادم DHCP.

---

### **6. (NAT - Network Address Translation)**

 - **Types of NAT:**
	1. **Static NAT:**
		كل private  IP بيتحول ل public IP ثابت بيستخدم مع السيرفرات علشان تبقي معروفة
	2. **Dynamic NAT:** 
		 بيبقي مجموعة (Pool) من public IPs كل private IP بياخد واحد من الايبهات دي بتبقي(Many-to-Many) بس المشكلة لو  الـ Pool خلصت مفيش اي private IP هيعرف يخرج من الشبكة.
	        
	3. **PAT (Port Address Translation) / NAT Overload:**
	     يستخدم ال Public IP  مع رقم الPort Number للتمييز بحيث انه كدا بقي يدعم عدد كبير(نظريا 65 ألف، عمليا 40 ألف بس) فكدا سمح لكذا Private IP يخرج ب Public IP واحد. و بيغير ال Port number  لو جهاز طلب يخرج ببورت محجوز من جهاز تاني .
	
	4. **Dynamic PAT:** 
		يجمع بين Dynamic NAT و PAT، بيبقي في Pool فيها  private IPs وكمان بيستخدم البورت.
	    

 - **Port Forwarding:**
	 هو عكس الـ PAT، اقدر اوصل لكذا سيرفر داخلي ب public IP واحد من خلال البورت
 
 - **VPN (Virtual Private Network):**
	- Intranet VPN: يربط شبكات الشركة الداخلية ببعضها.
	- Extranet VPN: يربط الشركة مع شركات أو عملاء خارجيين.

