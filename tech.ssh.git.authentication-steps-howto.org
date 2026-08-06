# GitHub SSH Authentication Setup Guide

This guide covers generating a secure SSH key, adding it to your system’s SSH agent, and linking it to your GitHub account.

---

## Step 1: Generate a New SSH Key
Open your terminal and run the following command. Replace the placeholder email with your GitHub account email. 

We use **Ed25519**, which is modern, highly secure, and faster than older RSA keys.

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### What to do during the prompts:
1. **Save File Location**: When it asks to *"Enter a file in which to save the key,"* simply press **Enter** to accept the default location (`~/.ssh/id_ed25519`).
2. **Passphrase**: Type a secure passphrase and press **Enter**, then type it again to confirm. 
   * *Note: The cursor will not move or show characters while typing passwords in the terminal. This is normal security behavior.*

---

## Step 2: Start the SSH Agent & Add the Key
The SSH agent manages your keys so you don't have to type your passphrase every single time you use git.

1. **Start the agent** in the background:
   ```bash
   eval "$(ssh-agent -s)"
   ```
2. **Add your private key** to the agent:
   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```

---

## Step 3: Copy Your Public Key
You need to copy the contents of your **public** key (`.pub`) to paste it into GitHub. Run the command that matches your operating system:

* **macOS**:
  ```bash
  pbcopy < ~/.ssh/id_ed25519.pub
  ```
* **Linux (requires xclip)**:
  ```bash
  xclip -sel clip < ~/.ssh/id_ed25519.pub
  ```
* **Windows (Git Bash / WSL)**:
  ```bash
  cat ~/.ssh/id_ed25519.pub | clip
  ```
* **Universal (Manual Copy)**: If the shortcuts above do not work, print the key to your terminal screen, highlight it completely, and copy it manually:
  ```bash
  cat ~/.ssh/id_ed25519.pub
  ```

---

## Step 4: Add the SSH Key to GitHub
1. Go to https://github.com and log in.
2. Click your profile photo in the upper-right corner, then click **Settings**.
3. In the left sidebar, click **SSH and GPG keys**.
4. Click the green **New SSH key** button.
5. In the **Title** field, type a memorable label for the machine (e.g., "Personal MacBook Pro" or "Ubuntu Desktop").
6. Leave the **Key type** as "Authentication Key".
7. Paste your key into the **Key** box.
8. Click **Add SSH key**. Confirm with your GitHub password if prompted.

---

## Step 5: Test the Connection
To ensure everything works perfectly, run this test command in your terminal:

```bash
ssh -T git@github.com
```

### What to expect:
1. You will see a warning like this:
   ```text
   The authenticity of host 'github.com (IP_ADDRESS)' can't be established.
   ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJLinexs5G4gLmW9s8at6FJvA36v0k.
   Are you sure you want to continue connecting (yes/no/[fingerprint])?
   ```
2. Type **`yes`** and press **Enter**.
3. If successful, you will see a friendly greeting:
   ```text
   Hi username! You've successfully authenticated, but GitHub does not provide shell access.
   ```

---

## Step 6: Update Existing Repositories (If Needed)
If you previously cloned repositories using **HTTPS** (URLs starting with `https://`), they will still ask for your password. You must switch them to use **SSH** URLs instead.

Inside your local project folder, run:
```bash
git remote set-url origin git@github.com:username/repository-name.git
```
*(Replace `username` and `repository-name` with your actual GitHub details).*

