✅ **Task 1:**  

On the serverb machine, ensure that newly created users must change their passwords every 30 days.

```bash
sudo sed -i 's/^PASS_MAX_DAYS\s\+[0-9]\+/PASS_MAX_DAYS   30/' /etc/login.defs
```
---
✅ **Task 2:**  

Create the consultants group with a GID of 35000.

```bash
groupadd -g 35000 consultants
```
---
✅ **Task 3:** 

Configure administrative rights to enable all consultants group members to execute any command as any user. Avoid using the visudo command-line tool to edit the /etc/sudoers file. Instead, place the configuration file in the /etc/sudoers.d directory.

```bash
echo "%consultants  ALL=(ALL) ALL" > /etc/sudoers.d/consultants
```
---
✅ **Task 4:** 

Create the consultant1, consultant2, and consultant3 users with the consultants group as their supplementary group.

```bash
useradd -G consultants consultant1
useradd -G consultants consultant2
useradd -G consultants consultant3
```
---
✅ **Task 5:** 

Set the consultant1, consultant2, and consultant3 passwords to redhat.

```bash
sudo -i
passwd consultant1
passwd consultant2
passwd consultant3
```

---
✅ **Task 6:** 

Set the consultant1, consultant2, and consultant3 accounts to expire 90 days from the current day.

```bash
date -d "+90 days" +%F

chage -E "90 days" consultant1
chage -E "90 days" consultant2
chage -E "90 days" consultant3
```

---
✅ **Task 7:** 

Change the password policy for the consultant2 account to require a new password every 15 days.


```bash
chage -M 15 consultant2
```

---
✅ **Task 8:** 

Additionally, force the consultant1, consultant2, and consultant3 users to change their passwords on the first login.

```bash
chage -d 0 consultant1
chage -d 0 consultant2
chage -d 0 consultant3
```
