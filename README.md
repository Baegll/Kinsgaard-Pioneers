This vault uses GitHub and the Obsidian Git plugin. Git stores the note history and shares changes with other users.

> [!WARNING]
> Git does not provide live editing. So in theory it can be an issue if we edit the same note at the same time, but it'll be fiiiiiine.
## Join the vault
1. Create a [GitHub account](https://github.com/).
2. Accept the invitation to this repository.
3. Install [Git](https://git-scm.com/downloads).
   - Install Git even if GitHub Desktop or GitHub CLI is installed.
   - On Windows, use the default installation options.
   - Make sure that Git Credential Manager is enabled.
   - Make sure that third-party software can use Git.
4. Close Obsidian and all terminal windows.
5. Open a new terminal window.
6. Make sure that Git is available:
```sh
   git --version
```
7. Clone the vault:
```sh
   git clone https://github.com/Baegll/Kinsgaard-Pioneers.git
```
8. Install [Obsidian](https://obsidian.md/) if it is not installed.
9. Open the cloned `Kinsgaard-Pioneers` folder as an Obsidian vault.
10. Open **Settings > Community plugins**.
11. Turn off **Restricted Mode**.
12. Install the **Git** plugin.
13. Enable the **Git** plugin.
## Configure the Git plugin
Open **Settings > Git**. Use these settings:
- Set **Auto commit-and-sync interval (minutes)** to `1`.
	- Note: Later we can set this to be a little  higher if we want, but I think constant sync is probably best for our use case.
- Set **Auto pull interval (minutes)** to `1`.
- Enable **Pull on startup**.
- Enable **Pull before push**.
- Enable **List filenames affected by commit in the commit body**.
- Set **Merge strategy** to **Rebase**.
- Set **Merge strategy on conflicts** to **None**.
- Enable **Squash commits before push**.
- Set **Author name for commit** to your name.
- Set **Author email for commit** to your email address.

The **None** conflict setting stops the sync when a conflict occurs. This setting prevents the plugin from discarding changes automatically. I'd recommend to avoid dealing with git merge headaches, we can set the conflict strategy to prefer our own notes.

You can use a [GitHub no-reply email address](https://docs.github.com/en/account-and-profile/how-tos/email-preferences/setting-your-commit-email-address). Use it if you do not want your personal email in the Git history.

On a desktop computer, you can set the author with these commands:
```sh
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
## Test the sync
1. Make a small change to a note.
2. Wait for the Git plugin to complete the sync.
3. Make sure that Obsidian does not show an error.
4. Make sure that the change is visible on [GitHub](https://github.com/Baegll/Kinsgaard-Pioneers).
The first clone, pull, or push can open a browser. Complete the GitHub sign-in process in the browser.

Do not use a GitHub account password for HTTPS Git authentication. Use Git Credential Manager or a personal access token.
## Initialize the repository (owner only)
Use this procedure only when the GitHub repository has no branch.
1. Make the initial vault commit.
2. Configure the `origin` remote.
3. Create `origin/main` and its tracking connection:
```sh
   git push -u origin main
```
4. Invite the other users after the push is complete.

If `git status` reports that `origin/main` is gone, make sure that the GitHub repository is empty. Then, run the push command above.

Do not remove the upstream configuration. Git needs this configuration for automatic pulls and pushes.
## Correct a sync error
1. Stop editing the vault.
2. Read the Obsidian Git error notification.
3. Open a terminal in the vault folder.
4. Run this command:
```sh
   git status
```
5. Contact the other editor if both users changed the same note.
6. Keep both versions of the note until you resolve the conflict.

> [!CAUTION]
> Try to avoid force push or reset to correct a sync error. These commands can delete note history.

A synchronized vault has these status messages:
- The `main` branch is up to date with `origin/main`.
- The working tree is clean.
## Use Obsidian
Use `[[double brackets]]` to create a note link. For example, use [[The K.T.S. Pioneer]] to link to the ship note.
## Check Git
The Git plugin does these operations:
1. It pulls commits from GitHub.
2. It commits local changes.
3. It pushes local commits to GitHub.
Use these commands to examine the vault. These commands do not change files:
```sh
git status
git log --oneline --decorate -10
```
Git ignores workspace layouts, trash, and operating-system cache files. Git tracks the shared `.obsidian` configuration for new users.
## Best practices
- Use `[[wikilinks]]` to connect related notes.
- Use frontmatter for structured metadata.
- Keep attachments in the vault.
- Let the sync complete before you close Obsidian.
- Let the sync complete before you use another device.
