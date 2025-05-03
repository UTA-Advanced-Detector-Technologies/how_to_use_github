# Table of Contents

- [Adding an SSH key to your account](#adding-an-ssh-key-to-your-account)
- [Cloning a GitHub Repo Using SSH](#cloning-a-github-repo-using-ssh)
- [Branches](#branches)
- [Switching Between Branches Safely](#switching-between-branches-safely)
- [Pushing Changes](#pushing-changes)
- [Pulling Changes](#pulling-changes)
- [How to add a default Github User](#how-to-add-a-default-github-user)
- [Pipeline for new contributions](#pipeline-for-new-contributions)

---
# Adding an SSH key to your account

Make sure to do this after installing Git (see next section)

1. **Open Terminal or Command Prompt:**
   - On macOS and Linux, open Terminal.
   - On Windows, open Command Prompt or Git Bash.

2. **Generate SSH key pair:**
   Tyoe the following command in your terminal after inserting your email into the command:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@someplace"
   ```
   This will give you a prompt like:
      'Generating public/private ed25519 key pair.
      Enter file in which to save the key (/Users/olivias-local/.ssh/id_ed25519):'
   Enter the file to save the key to, just copy what it gives you in the parenthesis. Then just press enter twice when it asks for a passphrase.
3. **Copy Key:**
   Now you can find the key by typing this in the command line:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   This will print something like:

      'ssh-ed25519 SOMERANDOMCHARACTERSTRINGblahblahblahblah your_email@someplace'

   Copy that
5. **Add key to GitHub:**
   Now add this key to your GitHub account by going to **Settings → SSH and GPG keys → New SSH key** and paste what you just copied
   
---
# Cloning a GitHub Repo Using SSH

To clone a GitHub repository, follow these steps:

1. **Install Git:**
   Ensure that Git is installed on your computer. You can download it from [git-scm.com](https://git-scm.com/) and follow the installation instructions for your operating system.

2. **Open Terminal or Command Prompt:**
   - On macOS and Linux, open Terminal.
   - On Windows, open Command Prompt or Git Bash.

3. **Navigate to the Desired Directory:**
   Use the `cd` command to navigate to the directory where you want to clone the repository. For example:
   ```bash
   cd path/to/your/directory
   ```
4. **Find the Repository URL:**
   Go to the GitHub page of the repository you want to clone. Click on the "Code" button and go to the "SSH" tab. Copy the URL provided there. It should look something like:
      `git@github.com:CosmiQuantum/how_to_use_github.git`
5. **Clone the Repository:**
   Use the `git clone` command followed by the repository URL. For example:
   ```bash
   git clone git@github.com:CosmiQuantum/how_to_use_github.git
   ```

7. **Verify the Clone:**
   After the clone process completes, navigate into the cloned repository folder:
   ```bash
   cd how_to_use_github
   ```
---
# Branches
1. **List Available Branches:**
   To view all branches in the repository, use the following command:
   ```bash
   git branch -a
   ```
2. **Create a New Branch:**
   To create a new branch (and switch to it), use:
   ```bash
   git checkout -b new-branch-name
   ```
---
# Switching Between Branches Safely

To switch between branches in Git without affecting the branch you're currently working on, follow these steps:

1. **Commit or Stash Changes:**
   Make sure you have no uncommitted changes on your current branch. You can either commit your changes using:
   ```bash
   git add .
   git commit -m "Your commit message"
   ```
2. **Switch Branch:**
   Switch branches by using one of the two following commands:
   ```bash
   git switch branch-name
   ```
   or:
   ```bash
   git checkout branch-name
   ```
3. **Verify Branch:**
   Make sure you are indeed on the right branch by doing:
   ```bash
   git branch
   ```
---
# Pushing Changes 

These instructions assume you have Git installed on your computer and have already cloned a repository.  If not, you'll need to do that first.

**Steps:**
1. **Open Terminal or Command Prompt**: Navigate to the local repository directory using the `cd` command.
   ```bash
   cd path/to/your/repository
   ```

2. **Stage your changes:**  Use `git add` to stage the files you want to include in your commit. You can add individual files, specific directories, or all changes using the following commands:

   * `git add <file>`  (e.g., `git add my_file.txt`)
   * `git add <directory>` (e.g., `git add my_directory/`)
   * `git add .` (stages all changes in the current directory and subdirectories)


3. **Commit your changes:** Use `git commit` to save your staged changes with a descriptive message.  This creates a snapshot of your work.

   ```bash
   git commit -m "Your descriptive commit message"
   ```
   Replace `"Your descriptive commit message"` with a nice summary of the
   changes you've made. 

4. **Push your changes:** Use `git push` to upload your committed changes to the
remote repository
   ```bash
   git push origin <branch_name>
   ```
   `origin` is typically the name of the remote repository. You can check the
   remote names using `git remote -v`.
   
   `<branch_name>` is the name of the branch you're working on. If you're pushing to a different branch, replace `<branch_name>`
   accordingly.

Example:

Let's say you've made changes to `my_file.txt` and `another_file.js`:

1. `git add my_file.txt another_file.js`
2. `git commit -m "Added new features and fixed a bug"`
3. `git push origin <branchname>`

---
# Pulling Changes

1. **Open Terminal or Command Prompt**: Navigate to the local repository directory using the `cd` command.
   ```bash
   cd path/to/your/repository
   ```

2. **Pull Changes:** Use this command to pull the latest changes from the remote repository.
   ```bash
   git pull origin your-branch-name
   ```
   Replace your-branch-name with the name of the branch you want to pull from.

3. **If this throws and error:** Probably someone has pushed changes to the repo, and you have not pulled them before making local changes. In this case do these steps:
   - Fetch the latest changes from the remote repository. This will update your local copy of the remote branches without merging:
      ```bash
      git fetch origin
      ```
   - Merge the changes into your current branch. If you are on the branch where you want to merge the changes, use:
      ```bash
      git merge origin/<branchname>
      ```
        Replace <branchname> with the name of the branch you are merging from. If there are any merge conflicts, Git will notify you here. You'll need to resolve those conflicts in your files and then stage the resolved files.
   - Commit the merge if it happens automatically or if you had to resolve conflicts:
      ```bash
      git commit -m "Merge updates from remote branch"
      ```
   - Push your changes to the remote repo:
     ```bash
     git push origin <branchname>
     ```
---
# How to add a default Github User

To remove the currently configured GitHub user in the command line and add a new one, use the following instructions. 

1. **Check Current Git Configuration:** Look at the current Git user settings using:
   ```bash
   git config --global user.name
   git config --global user.email
   ```

2. **Unset or Update Git User Information:** unset whatever settings are there now using:
   ```bash
   git config --global --unset user.name
   git config --global --unset user.email
   ```

3. **Set New User Information:** Set your username now by doing:
   ```bash
   git config --global user.name "New Username"
   git config --global user.email "newemail@example.com"
   ```
   *Replace `"New Username"` and `"newemail@example.com"` with your GitHub username and email.*

4. **Verify the Changes:** Ensure that your Git configuration and remote URLs are updated correctly.
   ```bash
   git config --global user.name
   git config --global user.email
   ```

---
# Pipeline for New Contributions

## 1. Open an Issue
1. Go to the `Issues` tab at the top of the GitHub Repo (next to the `<> Code` tab).  
2. Click on the green **New issue** button on the right of the page.  
3. Add a title for the issue describing generally the types of changes you want to make, such as _“Add charge parity QICK experiment”_. You can put a description if you want, but this is optional.  
4. Press the green **Create** button on the bottom right corner of the page.  
5. You should now see your issue, with a number next to it and a green bubble that says **Open** under the issue title.  

## 2. Create a Branch
1. On the far right of the issue page, find the blue **Create a branch** link under the **Development** header. Click it.  
2. In the popup:
   - Give your branch a name with your initials, hyphen, a descriptive title using camelCase with a lowercase first letter, hyphen, and then the branch number (which will automatically show up). For example:
     ```
     os-pipelineTest-2
     ```
   - For the **Branch source** tab, select the branch called `development` if you are being well-behaved.  
   - Make sure you are in the correct Repository :)  
   - Press the green **Create branch** button.  


## 3. Check Out Locally
If you’d like to work on that branch on your computer, run:
```bash
cd repo-name
git branch -r                   # to look at the branches that are remote
git fetch origin 
git checkout os-pipelineTest-2  # switch to the branch you made
git branch                      # make sure you are on the correct branch
```

## 4. Develop & Sync

1. Make all of your changes on this branch, then commit and push them.
2. If the base branch has updates from other users while you are editing, you can run:

   ```bash
   git merge origin/development
   ```

   or

   ```bash
   git pull origin development
   ```

## 5. Open a Pull Request

1. Go to your repository on GitHub and click the **Pull requests** tab (right next to **Issues**).
2. Click **New pull request**.
3. Set the **base:** dropdown to the branch you originally branched off (e.g. `development`), and the **compare:** dropdown to your feature branch (e.g. `os-pipelineTest-2`).
4. Scroll down to make sure your changes look correct.
5. Click **Create pull request**.
6. Fill in:

   * A concise **title** (e.g. “Add pipeline issue template”).
   * A brief **description** explaining what you’ve done and why.
7. Click **Create pull request** again to finalize.
8. Once reviewers approve, click **Merge pull request**, choose your merge method (e.g. “Squash and merge”), and confirm.
9. After merging, you can safely delete your feature branch by clicking **Delete branch** on the PR page.






