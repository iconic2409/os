Various LINUX command:
#!/bin/bash

# ----------------------------------------#ê´‘
ê´’ File and Directory Management
# -----------------------------------------

pwd

# 1. Show current working directory

ls -lart

# 2. List all ï¬les, long format, reverse me

cd /path/to/dir

# 3. Change directory

mkdir my_folder

# 4. Create a new folder

touch newï¬le.txt

# 5. Create an empty ï¬le

cp ï¬le1.txt ï¬le2.txt # 6. Copy ï¬le1 to ï¬le2
mv ï¬le.txt /dest/
rm ï¬le.txt
du -sh folder/
df -h

# 7. Move or rename a ï¬le
# 8. Delete a ï¬le
# 9. Show folder size

# 10. Disk usage (human-readable)

# ----------------------------------------#è¹§
è¹ª User and System Informa on
è¹©
è¹¨
# -----------------------------------------

whoami

# 11. Show current username

logname

# 12. Show login name

hostname

# 13. Show system hostname

uname -a

# 14. Full OS and kernel info

up me

# 15. Show how long the system has been running

# ----------------------------------------# ê»© Process and System Monitoring
# -----------------------------------------

htop

# 16. Interac ve process viewer (if installed)

ps aux

# 17. Snapshot of running processes

shutdown +10

# 18. Schedule shutdown in 10 minutes

shutdown -c

# 19. Cancel scheduled shutdown

# ----------------------------------------#êº™
êº˜ Permissions & Ownership
êº›
êºš
# -----------------------------------------

chmod 755 script.sh

# 20. Change permissions (rwxr-xr-x)

chown user:group ï¬le # 21. Change owner and group

#êº™
êº˜ CHMOD EXPLAINED:
êº›
êºš
# Read = 4, Write = 2, Execute = 1
# User: 7 (rwx), Group: 5 (r-x), Others: 5 (r-x)
# chmod 755 = rwxr-xr-x

# ----------------------------------------#ê´˜
ê¶¬ Text Editors
ê¶«
ê¶ª
ê¶©
ê¶¨
ê´›
ê´š
ê´™
# -----------------------------------------

nano ï¬le.txt

# 22. Beginner-friendly terminal editor

vim ï¬le.txt

# 23. Advanced terminal editor (i=insert, :wq=save+quit)

# ----------------------------------------#í©¯
í©± Help and Info
í©°
# -----------------------------------------

man ls

# 24. View manual/help page for a command

history

# 25. Show your command history

clear

# 26. Clear the terminal screen

# ----------------------------------------#í®
í®Ž Aliases and Conï¬gura on
í®
# -----------------------------------------

alias ll='ls -lart'

# 27. Create shortcut for a command

unalias ll

# 28. Remove an alias temporarily

source ~/.bashrc

# 29. Reload bash conï¬g

echo $SHELL

# 30. Show current shell being used

OS TYPE AND ALL :
#!/bin/bash

# i) Display OS version, release number and kernel version
echo "OS Version

: $(uname -o)"

echo "Kernel Version : $(uname -r)"
echo "Release Number : $(cat /etc/os-release | grep VERSION)"

# ii) Display top 10 processors in memory descending order
echo -e "\nTop 10 processes by CPU usage:"
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 11

# iii) Display current logged in user & log name
echo -e "\nCurrent User
echo "Logged Name

: $(whoami)"

: $(logname)"

# iv) Display 10 processes with highest memory usage
echo -e "\nTop 10 processes by Memory usage:"
ps -eo pid,comm,%mem --sort=-%mem | head -n 11

# v) Display current shell home directory, O.S. Type, current path
echo -e "\nCurrent Shell Home Directory: $HOME"
echo "OS Type
echo "Current Path

: $(uname -s)"
: $PATH"

Copy :
#include <stdio.h>
#include <stdlib.h>

int main() {
FILE *fptr1, *fptr2;
char ï¬lename[100], c;

prin ("Enter the ï¬lename to open for reading\n");
scanf("%s", ï¬lename);

fptr1 = fopen(ï¬lename, "r");
if (fptr1 == NULL) {
prin ("Cannot open ï¬le %s\n", ï¬lename);
exit(0);
}

prin ("Enter the ï¬lename to open for wri ng\n");
scanf("%s", ï¬lename);

fptr2 = fopen(ï¬lename, "w");
if (fptr2 == NULL) {
prin ("Cannot open ï¬le %s\n", ï¬lename);
exit(0);

}

c = fgetc(fptr1);
while (c != EOF) {
fputc(c, fptr2);
c = fgetc(fptr1);
}

prin ("\nContents copied to %s\n", ï¬lename);
fclose(fptr1);
fclose(fptr2);
return 0;
}

Move :
#include <stdio.h>

int main() {
char oldname[100], newname[100];

prin ("Enter the source ï¬le name: ");
scanf("%s", oldname);

prin ("Enter the des na on ï¬le name (with path if needed): ");
scanf("%s", newname);

if (rename(oldname, newname) == 0)
prin ("File moved/renamed successfully.\n");
else
perror("Error moving ï¬le");

return 0;
}

List :
#include <stdio.h>
#include <dirent.h>

int main() {
struct dirent *de;
DIR *dr = opendir(".");

if (dr == NULL) {
prin ("Could not open current directory\n");
return 0;
}

prin ("Files in current directory:\n");
while ((de = readdir(dr)) != NULL)
prin ("%s\n", de->d_name);

closedir(dr);
return 0;
}

Fork :
#include <stdio.h>
#include <unistd.h> // For fork(), getpid(), and getppid()
#include <stdlib.h> // For exit()

int main() {
pid_t pid;
// Create a child process using fork()
pid = fork();

if (pid < 0) {
// Error occurred
perror("fork failed");
exit(1);
} else if (pid == 0) {
// This block is executed by the child process
prin ("Child Process:\n");
prin ("Child PID: %d\n", getpid());
prin ("Parent PID: %d\n", getppid());
} else {
// This block is executed by the parent process
prin ("Parent Process:\n");
prin ("Parent PID: %d\n", getpid());
prin ("Child PID: %d\n", pid);
}
return 0;
}

Semaphore:
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>
#deï¬ne SIZE 5
int buï¬€er[SIZE];
int in = 0, out = 0;
sem_t empty; // Counts empty buï¬€er slots
sem_t full; // Counts full buï¬€er slots
pthread_mutex_t mutex; // Ensures mutual exclusion
void* producer(void* arg) {
int item, i;
for (i = 0; i < 10; i++) {
item = rand() % 100; // Produce a random item
sem_wait(&empty);

// Decrease empty count

pthread_mutex_lock(&mutex); // Enter cri cal sec on

buï¬€er[in] = item;
prin ("Producer produced: %d at %d\n", item, in);
in = (in + 1) % SIZE;

pthread_mutex_unlock(&mutex); // Exit cri cal sec on
sem_post(&full);
sleep(1);
}

// Increase full count

// Simulate me taken to produce

pthread_exit(NULL);
}
void* consumer(void* arg) {
int item, i;
for (i = 0; i < 10; i++) {
sem_wait(&full);

// Decrease full count

pthread_mutex_lock(&mutex); // Enter cri cal sec on

item = buï¬€er[out];
prin ("Consumer consumed: %d from %d\n", item, out);
out = (out + 1) % SIZE;

pthread_mutex_unlock(&mutex); // Exit cri cal sec on
sem_post(&empty);
sleep(2);

// Increase empty count

// Simulate me taken to consume

}
pthread_exit(NULL);
}
int main() {
pthread_t prod, cons; // Ini alize semaphores and mutex
sem_init(&empty, 0, SIZE); // All slots are ini ally empty
sem_init(&full, 0, 0);

// No items ini ally

pthread_mutex_init(&mutex, NULL);
// Create threads
pthread_create(&prod, NULL, producer, NULL);
pthread_create(&cons, NULL, consumer, NULL);
// Wait for threads to ï¬nish
pthread_join(prod, NULL);

pthread_join(cons, NULL);
// Cleanup
sem_destroy(&empty);
sem_destroy(&full);
pthread_mutex_destroy(&mutex);
return 0;
}

BEST WORST FIRT FIT:
#include <stdio.h>
#deï¬ne MAX 10

void ï¬rstFit(int blockSize[], int m, int processSize[], int n) {
int alloca on[MAX];
for (int i = 0; i < n; i++)
alloca on[i] = -1;

for (int i = 0; i < n; i++) {
for (int j = 0; j < m; j++) {
if (blockSize[j] >= processSize[i]) {
alloca on[i] = j;
blockSize[j] -= processSize[i];
break;
}
}
}

prin ("\nFirst Fit:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d (%d KB) --> ", i + 1, processSize[i]);
if (alloca on[i] != -1)
prin ("Block %d\n", alloca on[i] + 1);
else
prin ("Not Allocated\n");
}

}

void bestFit(int blockSize[], int m, int processSize[], int n) {
int alloca on[MAX];
for (int i = 0; i < n; i++)
alloca on[i] = -1;

for (int i = 0; i < n; i++) {
int bestIdx = -1;
for (int j = 0; j < m; j++) {
if (blockSize[j] >= processSize[i]) {
if (bestIdx == -1 || blockSize[j] < blockSize[bestIdx])
bestIdx = j;
}
}

if (bestIdx != -1) {
alloca on[i] = bestIdx;
blockSize[bestIdx] -= processSize[i];
}
}

prin ("\nBest Fit:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d (%d KB) --> ", i + 1, processSize[i]);
if (alloca on[i] != -1)
prin ("Block %d\n", alloca on[i] + 1);
else

prin ("Not Allocated\n");
}
}

void worstFit(int blockSize[], int m, int processSize[], int n) {
int alloca on[MAX];
for (int i = 0; i < n; i++)
alloca on[i] = -1;

for (int i = 0; i < n; i++) {
int worstIdx = -1;
for (int j = 0; j < m; j++) {
if (blockSize[j] >= processSize[i]) {
if (worstIdx == -1 || blockSize[j] > blockSize[worstIdx])
worstIdx = j;
}
}

if (worstIdx != -1) {
alloca on[i] = worstIdx;
blockSize[worstIdx] -= processSize[i];
}
}

prin ("\nWorst Fit:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d (%d KB) --> ", i + 1, processSize[i]);
if (alloca on[i] != -1)

prin ("Block %d\n", alloca on[i] + 1);
else
prin ("Not Allocated\n");
}
}

int main() {
int blockSize[MAX], processSize[MAX];
int m, n;

prin ("Enter number of memory blocks: ");
scanf("%d", &m);
prin ("Enter size of each block:\n");
for (int i = 0; i < m; i++) {
prin ("Block %d: ", i + 1);
scanf("%d", &blockSize[i]);
}

prin ("Enter number of processes: ");
scanf("%d", &n);
prin ("Enter size of each process:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d: ", i + 1);
scanf("%d", &processSize[i]);
}

int b1[MAX], b2[MAX], b3[MAX];
for (int i = 0; i < m; i++) {

b1[i] = blockSize[i];
b2[i] = blockSize[i];
b3[i] = blockSize[i];
}

ï¬rstFit(b1, m, processSize, n);
bestFit(b2, m, processSize, n);
worstFit(b3, m, processSize, n);

return 0;
}

Various LINUX command:
#!/bin/bash

# ----------------------------------------#ê´‘
ê´’ File and Directory Management
# -----------------------------------------

pwd

# 1. Show current working directory

ls -lart

# 2. List all ï¬les, long format, reverse me

cd /path/to/dir

# 3. Change directory

mkdir my_folder

# 4. Create a new folder

touch newï¬le.txt

# 5. Create an empty ï¬le

cp ï¬le1.txt ï¬le2.txt # 6. Copy ï¬le1 to ï¬le2
mv ï¬le.txt /dest/
rm ï¬le.txt
du -sh folder/
df -h

# 7. Move or rename a ï¬le
# 8. Delete a ï¬le
# 9. Show folder size

# 10. Disk usage (human-readable)

# ----------------------------------------#è¹§
è¹ª User and System Informa on
è¹©
è¹¨
# -----------------------------------------

whoami

# 11. Show current username

logname

# 12. Show login name

hostname

# 13. Show system hostname

uname -a

# 14. Full OS and kernel info

up me

# 15. Show how long the system has been running

# ----------------------------------------# ê»© Process and System Monitoring
# -----------------------------------------

htop

# 16. Interac ve process viewer (if installed)

ps aux

# 17. Snapshot of running processes

shutdown +10

# 18. Schedule shutdown in 10 minutes

shutdown -c

# 19. Cancel scheduled shutdown

# ----------------------------------------#êº™
êº˜ Permissions & Ownership
êº›
êºš
# -----------------------------------------

chmod 755 script.sh

# 20. Change permissions (rwxr-xr-x)

chown user:group ï¬le # 21. Change owner and group

#êº™
êº˜ CHMOD EXPLAINED:
êº›
êºš
# Read = 4, Write = 2, Execute = 1
# User: 7 (rwx), Group: 5 (r-x), Others: 5 (r-x)
# chmod 755 = rwxr-xr-x

# ----------------------------------------#ê´˜
ê¶¬ Text Editors
ê¶«
ê¶ª
ê¶©
ê¶¨
ê´›
ê´š
ê´™
# -----------------------------------------

nano ï¬le.txt

# 22. Beginner-friendly terminal editor

vim ï¬le.txt

# 23. Advanced terminal editor (i=insert, :wq=save+quit)

# ----------------------------------------#í©¯
í©± Help and Info
í©°
# -----------------------------------------

man ls

# 24. View manual/help page for a command

history

# 25. Show your command history

clear

# 26. Clear the terminal screen

# ----------------------------------------#í®
í®Ž Aliases and Conï¬gura on
í®
# -----------------------------------------

alias ll='ls -lart'

# 27. Create shortcut for a command

unalias ll

# 28. Remove an alias temporarily

source ~/.bashrc

# 29. Reload bash conï¬g

echo $SHELL

# 30. Show current shell being used

OS TYPE AND ALL :
#!/bin/bash

# i) Display OS version, release number and kernel version
echo "OS Version

: $(uname -o)"

echo "Kernel Version : $(uname -r)"
echo "Release Number : $(cat /etc/os-release | grep VERSION)"

# ii) Display top 10 processors in memory descending order
echo -e "\nTop 10 processes by CPU usage:"
ps -eo pid,comm,%cpu --sort=-%cpu | head -n 11

# iii) Display current logged in user & log name
echo -e "\nCurrent User
echo "Logged Name

: $(whoami)"

: $(logname)"

# iv) Display 10 processes with highest memory usage
echo -e "\nTop 10 processes by Memory usage:"
ps -eo pid,comm,%mem --sort=-%mem | head -n 11

# v) Display current shell home directory, O.S. Type, current path
echo -e "\nCurrent Shell Home Directory: $HOME"
echo "OS Type
echo "Current Path

: $(uname -s)"
: $PATH"

Copy :
#include <stdio.h>
#include <stdlib.h>

int main() {
FILE *fptr1, *fptr2;
char ï¬lename[100], c;

prin ("Enter the ï¬lename to open for reading\n");
scanf("%s", ï¬lename);

fptr1 = fopen(ï¬lename, "r");
if (fptr1 == NULL) {
prin ("Cannot open ï¬le %s\n", ï¬lename);
exit(0);
}

prin ("Enter the ï¬lename to open for wri ng\n");
scanf("%s", ï¬lename);

fptr2 = fopen(ï¬lename, "w");
if (fptr2 == NULL) {
prin ("Cannot open ï¬le %s\n", ï¬lename);
exit(0);

}

c = fgetc(fptr1);
while (c != EOF) {
fputc(c, fptr2);
c = fgetc(fptr1);
}

prin ("\nContents copied to %s\n", ï¬lename);
fclose(fptr1);
fclose(fptr2);
return 0;
}

Move :
#include <stdio.h>

int main() {
char oldname[100], newname[100];

prin ("Enter the source ï¬le name: ");
scanf("%s", oldname);

prin ("Enter the des na on ï¬le name (with path if needed): ");
scanf("%s", newname);

if (rename(oldname, newname) == 0)
prin ("File moved/renamed successfully.\n");
else
perror("Error moving ï¬le");

return 0;
}

List :
#include <stdio.h>
#include <dirent.h>

int main() {
struct dirent *de;
DIR *dr = opendir(".");

if (dr == NULL) {
prin ("Could not open current directory\n");
return 0;
}

prin ("Files in current directory:\n");
while ((de = readdir(dr)) != NULL)
prin ("%s\n", de->d_name);

closedir(dr);
return 0;
}

Fork :
#include <stdio.h>
#include <unistd.h> // For fork(), getpid(), and getppid()
#include <stdlib.h> // For exit()

int main() {
pid_t pid;
// Create a child process using fork()
pid = fork();

if (pid < 0) {
// Error occurred
perror("fork failed");
exit(1);
} else if (pid == 0) {
// This block is executed by the child process
prin ("Child Process:\n");
prin ("Child PID: %d\n", getpid());
prin ("Parent PID: %d\n", getppid());
} else {
// This block is executed by the parent process
prin ("Parent Process:\n");
prin ("Parent PID: %d\n", getpid());
prin ("Child PID: %d\n", pid);
}
return 0;
}

Semaphore:
#include <stdio.h>
#include <stdlib.h>
#include <pthread.h>
#include <semaphore.h>
#include <unistd.h>
#deï¬ne SIZE 5
int buï¬€er[SIZE];
int in = 0, out = 0;
sem_t empty; // Counts empty buï¬€er slots
sem_t full; // Counts full buï¬€er slots
pthread_mutex_t mutex; // Ensures mutual exclusion
void* producer(void* arg) {
int item, i;
for (i = 0; i < 10; i++) {
item = rand() % 100; // Produce a random item
sem_wait(&empty);

// Decrease empty count

pthread_mutex_lock(&mutex); // Enter cri cal sec on

buï¬€er[in] = item;
prin ("Producer produced: %d at %d\n", item, in);
in = (in + 1) % SIZE;

pthread_mutex_unlock(&mutex); // Exit cri cal sec on
sem_post(&full);
sleep(1);
}

// Increase full count

// Simulate me taken to produce

pthread_exit(NULL);
}
void* consumer(void* arg) {
int item, i;
for (i = 0; i < 10; i++) {
sem_wait(&full);

// Decrease full count

pthread_mutex_lock(&mutex); // Enter cri cal sec on

item = buï¬€er[out];
prin ("Consumer consumed: %d from %d\n", item, out);
out = (out + 1) % SIZE;

pthread_mutex_unlock(&mutex); // Exit cri cal sec on
sem_post(&empty);
sleep(2);

// Increase empty count

// Simulate me taken to consume

}
pthread_exit(NULL);
}
int main() {
pthread_t prod, cons; // Ini alize semaphores and mutex
sem_init(&empty, 0, SIZE); // All slots are ini ally empty
sem_init(&full, 0, 0);

// No items ini ally

pthread_mutex_init(&mutex, NULL);
// Create threads
pthread_create(&prod, NULL, producer, NULL);
pthread_create(&cons, NULL, consumer, NULL);
// Wait for threads to ï¬nish
pthread_join(prod, NULL);

pthread_join(cons, NULL);
// Cleanup
sem_destroy(&empty);
sem_destroy(&full);
pthread_mutex_destroy(&mutex);
return 0;
}

BEST WORST FIRT FIT:
#include <stdio.h>
#deï¬ne MAX 10

void ï¬rstFit(int blockSize[], int m, int processSize[], int n) {
int alloca on[MAX];
for (int i = 0; i < n; i++)
alloca on[i] = -1;

for (int i = 0; i < n; i++) {
for (int j = 0; j < m; j++) {
if (blockSize[j] >= processSize[i]) {
alloca on[i] = j;
blockSize[j] -= processSize[i];
break;
}
}
}

prin ("\nFirst Fit:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d (%d KB) --> ", i + 1, processSize[i]);
if (alloca on[i] != -1)
prin ("Block %d\n", alloca on[i] + 1);
else
prin ("Not Allocated\n");
}

}

void bestFit(int blockSize[], int m, int processSize[], int n) {
int alloca on[MAX];
for (int i = 0; i < n; i++)
alloca on[i] = -1;

for (int i = 0; i < n; i++) {
int bestIdx = -1;
for (int j = 0; j < m; j++) {
if (blockSize[j] >= processSize[i]) {
if (bestIdx == -1 || blockSize[j] < blockSize[bestIdx])
bestIdx = j;
}
}

if (bestIdx != -1) {
alloca on[i] = bestIdx;
blockSize[bestIdx] -= processSize[i];
}
}

prin ("\nBest Fit:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d (%d KB) --> ", i + 1, processSize[i]);
if (alloca on[i] != -1)
prin ("Block %d\n", alloca on[i] + 1);
else

prin ("Not Allocated\n");
}
}

void worstFit(int blockSize[], int m, int processSize[], int n) {
int alloca on[MAX];
for (int i = 0; i < n; i++)
alloca on[i] = -1;

for (int i = 0; i < n; i++) {
int worstIdx = -1;
for (int j = 0; j < m; j++) {
if (blockSize[j] >= processSize[i]) {
if (worstIdx == -1 || blockSize[j] > blockSize[worstIdx])
worstIdx = j;
}
}

if (worstIdx != -1) {
alloca on[i] = worstIdx;
blockSize[worstIdx] -= processSize[i];
}
}

prin ("\nWorst Fit:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d (%d KB) --> ", i + 1, processSize[i]);
if (alloca on[i] != -1)

prin ("Block %d\n", alloca on[i] + 1);
else
prin ("Not Allocated\n");
}
}

int main() {
int blockSize[MAX], processSize[MAX];
int m, n;

prin ("Enter number of memory blocks: ");
scanf("%d", &m);
prin ("Enter size of each block:\n");
for (int i = 0; i < m; i++) {
prin ("Block %d: ", i + 1);
scanf("%d", &blockSize[i]);
}

prin ("Enter number of processes: ");
scanf("%d", &n);
prin ("Enter size of each process:\n");
for (int i = 0; i < n; i++) {
prin ("Process %d: ", i + 1);
scanf("%d", &processSize[i]);
}

int b1[MAX], b2[MAX], b3[MAX];
for (int i = 0; i < m; i++) {

b1[i] = blockSize[i];
b2[i] = blockSize[i];
b3[i] = blockSize[i];
}

ï¬rstFit(b1, m, processSize, n);
bestFit(b2, m, processSize, n);
worstFit(b3, m, processSize, n);

return 0;
}


