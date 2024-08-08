# Project Setup Instructions

## Task Description

The Nautilus development team started with new project development. They have created different Git repositories to manage respective project's source code. One of the repositories, `/opt/cluster.git`, was created recently. The team has provided a sample `index.html` file that is currently present on the jump host under `/tmp`. The repository has been cloned at `/usr/src/kodekloudrepos` on the storage server in Stratos DC.

Your task is to copy the sample `index.html` file from the jump host to the storage server under the cloned repository at `/usr/src/kodekloudrepos`, add/commit the file, and push it to the master branch.

## Instructions

### 1. Copy the `index.html` file from the jump host to the storage server:

**Command:**
```bash
scp /tmp/index.html username@storage_server:/tmp/
Explanation:

scp stands for Secure Copy Protocol. It's used to securely transfer files between computers over a network.
/tmp/index.html is the path to the file on the jump host that you want to copy.
username@storage_server is where you're sending the file. Replace username with your actual username on the storage server, and storage_server with the address or name of the storage server.
:/tmp/ is the directory on the storage server where the file will be placed.
```
#### 2. Move the index.html file to the repository directory on the storage server:
```Command:

bash
Copy code
mv /tmp/index.html /usr/src/kodekloudrepos/
Explanation:

mv stands for move. It moves files or directories from one location to another.
/tmp/index.html is the current location of the file on the storage server (where you copied it to).
/usr/src/kodekloudrepos/ is the directory where you want to move the file. This is the directory where the Git repository is located.
```
##### 3. Navigate to the repository directory:
```Command:

bash
Copy code
cd /usr/src/kodekloudrepos
Explanation:

cd stands for change directory. It changes your current working directory to the specified one.
/usr/src/kodekloudrepos is the path to the directory you want to work in. This is where the Git repository is located.
```
#### 4. Add the index.html file to the staging area:
```Command:

bash
Copy code
git add index.html
```
### 5. Commit the changes:
```Command:

bash
Copy code
git commit -m "Add index.html to repository"
```
## 6. Push the changes to the master branch:
```Command:

bash
Copy code
git push origin master
```
