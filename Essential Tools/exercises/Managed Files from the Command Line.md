✅ **Task 1:**  

Create a directory named project_plans in the Documents directory. The Documents directory is placed in the student user's home directory. Create two empty files in the `project_plans` directory named `season1_project_plan.odf` and `season2_project_plan.odf`.

```bash
mkdir -p ~/Documents/project_plans
touch ~/Documents/project_plans/season{1,2}_project_plan.odf
```
```bash
ls -lR ~/Documents/
```

✅ **Task 2:**  
Create sets of empty practice files to use in this lab. If you do not immediately recognize the intended shell expansion shortcut, then use the solution to learn and practice. Use shell tab completion to locate file path names.

Create 12 files with `tv_seasonX_episodeY.ogg names` in the `/home/student` directory. Replace the `X` placeholder with the season number and the `Y` placeholder with that season's episode, for two seasons of six episodes each.

```bash

```

✅ **Task 3:** 

As the author of a successful series of mystery novels, you are editing your next bestseller's chapters for publishing. Create eight files with mystery_chapterX.odf names. Replace the X placeholder with the numbers 1 through 8.

✅ **Task 4:** 

Use a single command to create the ~/Videos/season1 and ~/Videos/season2 directories to organize the TV episodes. Move the appropriate TV episodes into the season subdirectories. Use only two commands, and specify destinations with relative syntax.

✅ **Task 5:** 

Create a two-level directory hierarchy with a single command to organize the mystery book chapters. Create the my_bestseller subdirectory under the Documents directory, and create the chapters subdirectory under the new my_bestseller directory. Create three more subdirectories directly under the my_bestseller directory with a single command. Name these subdirectories editor, changes, and vacation. You do not need to use the mkdir -p command to create parents because the my_bestseller parent directory exists.

✅ **Task 6:** 

Change to the chapters directory. Use the tilde (~) home directory shortcut to move all book chapters to the chapters directory, which is now your current directory. Use the simplest syntax to specify the destination directory.

You want to send the first two chapters to the editor for review. Move only those two chapters to the editor directory to avoid modifying them during the review. Starting from the chapters subdirectory, use brace expansion with a range to specify the chapter file names to move and a relative path for the destination directory.

While on vacation, you intend to write chapters 7 and 8. Use a single command to move the files from the chapters directory to the vacation directory. Specify the chapter file names by using brace expansion with a list of strings and without using wildcard characters.

✅ **Task 7:** 

Change your working directory to ~/Videos/season2, and then copy the first episode of the season to the vacation directory. Use a single cd command to change from your working directory to the ~/Documents/my_bestseller/vacation directory. List its files. Use the previous working directory argument to return to the season2 directory. This argument succeeds if the last directory change with the cd command used only one command rather than several cd commands. From the season2 directory, copy the episode 2 file into the vacation directory. Use the shortcut again to return to the vacation directory.

✅ **Task 8:** 

The authors of chapters 5 and 6 want to experiment with possible changes. Copy both files from the ~/Documents/my_bestseller/chapters directory to the ~/Documents/my_bestseller/changes directory to prevent these changes from modifying original files.

Go to the ~/Documents/my_bestseller directory. Use square-bracket pattern matching to specify which chapter numbers to match in the filename argument of the cp command.

✅ **Task 9:**

Change your current directory to the changes direct
ory and use the date +%F command with command substitution to copy the mystery_chapter5.odf file to a new file that includes the full date. Use the mystery_chapter5_YYYY-MM-DD.odf name format.

By using command substitution with the date +%s command, make another copy of the mystery_chapter5.odf file, and append the current time stamp (as the number of seconds since the epoch, 1970-01-01 00:00 UTC) to ensure a unique file name.

✅ **Task 10:**

After further review, you decide that you do not need the plot changes. Delete the changes directory.

If it is necessary, then go to the changes directory and delete all the files in the directory. You cannot delete a directory when it is the current working directory.

Change to the parent directory of the changes directory. Try to delete the empty directory by using the rm command without the -r recursive option. This attempt should fail. Finally, use the rmdir command to delete the empty directory, which succeeds.

When the vacation is over, you no longer need the vacation directory. Delete it by using the rm command with the recursive option.

When finished, return to the student user's home directory.

✅ **Task 11:**

Create a hard link to the ~/Documents/project_plans/season2_project_plan.odf file named ~/Documents/backups/season2_project_plan.odf.back. A hard link protects against accidental deletion of the original file and keeps the backup file updated as you change the original file.

Hint: If the ~/Documents/backups directory does not exist, then use the mkdir command to create it.

```bash
```