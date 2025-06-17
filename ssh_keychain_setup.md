# 🔐 Permanent SSH Key Setup with macOS Keychain Support

This guide explains how to permanently add an SSH key with a passphrase to the SSH agent and keychain on macOS, and how to suppress related deprecation warnings.

## ❓ Why These Steps?

- ✅ **Convenience**: Avoid entering the SSH passphrase every time.
- 🍏 **macOS Compatibility**: Modern macOS versions deprecated `-K` and `-A` options in `ssh-add`. Instead, it uses Apple-specific flags and environment variables.
- 🔒 **Security**: Securely store the SSH key's passphrase in the macOS keychain.
- 🚀 **Productivity**: Streamlines the workflow for developers working with Git, remote servers, and secure shell access.

---

## ⚠️ Deprecation Warning Message

When using older `ssh-add` commands like `ssh-add -K`, you may encounter the following warning:

```text
The -K and -A flags are deprecated and have been replaced
         by the --apple-use-keychain and --apple-load-keychain
         flags, respectively.  To suppress this warning, set the
         environment variable APPLE_SSH_ADD_BEHAVIOR as described in
         the ssh-add(1) manual page.
```

This means macOS now expects you to use `--apple-use-keychain` instead of the older flags.

---

## 🛠️ Step 1: Set Environment Variable to Suppress Deprecation Warning

In your shell configuration file (e.g., `~/.zshrc`, `~/.bash_profile`, etc.), add the following line:

```bash
export APPLE_SSH_ADD_BEHAVIOR=USE_KEYCHAIN
```

Reload the shell:

```bash
source ~/.zshrc  # or ~/.bash_profile depending on your shell
```

This tells macOS to use the keychain when adding keys and prevents warning messages.

---

## 🗝️ Step 2: Store Passphrase in macOS Keychain

Use the following command to add your SSH key to the keychain:

```bash
ssh-add --apple-use-keychain ~/.ssh/id_rsa
```

> 💡 Replace `id_rsa` with your actual SSH key filename if different (e.g., `id_ed25519`).

You’ll be prompted for your passphrase one final time. After that, it will be stored securely in the macOS keychain.

---

## ⚙️ Step 3: Automatically Add Key on Login

Edit (or create) your SSH config file:

```bash
nano ~/.ssh/config
```

Add the following content:

```ssh
Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
```

This configuration ensures your key is loaded automatically and the passphrase is retrieved from the keychain.

---

## 🧠 Step 4: Ensure SSH Agent is Running

macOS typically starts the SSH agent automatically. But if you ever need to ensure it's running:

```bash
eval "$(ssh-agent -s)"
```

This starts the agent manually and prepares it to load stored keys.

---

