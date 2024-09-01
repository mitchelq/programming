#### Created: 2024-09-01
#### Tags: [[Git]] [[GitLab]] [[MacBook]] [[Project Setup]]
#### Links: [[Version Control]] [[Terminal Usage]] [[SSH Keys]]

# Setting Up a Git Project on a New MacBook

## Overview
This guide will walk you through the process of setting up and cloning a Git project on your new MacBook.

## Steps

### 1. Install Git (if not already installed)

MacOS usually comes with Git pre-installed. To check, open Terminal and run:

```bash
git --version
```

If Git is not installed, you'll be prompted to install it.

### 2. Configure Git

Set up your Git identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@company.com"
```

### 3. Set Up SSH Key (Recommended)

1. Generate a new SSH key:
   ```bash
   ssh-keygen -t ed25519 -C "your.email@company.com"
   ```
   Press Enter to accept the default file location and optionally set a passphrase.

2. Start the SSH agent:
   ```bash
   eval "$(ssh-agent -s)"
   ```

3. Add your SSH key to the agent:
   ```bash
   ssh-add ~/.ssh/id_ed25519
   ```

4. Copy your public key:
   ```bash
   pbcopy < ~/.ssh/id_ed25519.pub
   ```

5. Add this key to your GitLab account:
   - Go to GitLab > Preferences > SSH Keys
   - Paste your key and save

### 4. Clone the Repository

1. Get the SSH URL of your project from GitLab.

2. In Terminal, navigate to where you want to clone the project:
   ```bash
   cd ~/Documents/Projects
   ```

3. Clone the repository:
   ```bash
   git clone git@gitlab.com:your-company/your-project.git
   ```

4. Navigate into the project directory:
   ```bash
   cd your-project
   ```

### 5. Set Up Project-Specific Configurations

1. Check if there's a README or setup guide in the project.

2. Install necessary dependencies (e.g., for a Node.js project):
   ```bash
   npm install
   ```

## Key Points
- Always use your company email for work-related Git configurations.
- SSH is more secure and convenient than HTTPS for Git operations.
- Check your company's specific guidelines for any additional setup steps.

## Best Practices
- Keep your SSH key passphrase secure and don't share it.
- Regularly update Git to the latest version.
- Familiarize yourself with your company's Git workflow and branching strategy.

## Common Pitfalls
- Ensure you have the necessary permissions to clone the repository.
- Double-check that you're using the correct SSH URL when cloning.
- If you encounter issues, ensure your SSH key is correctly added to your GitLab account.

## Related Concepts
- [[Git Branching Strategies]]
- [[GitLab CI/CD]]
- [[Code Review Process]]

## Additional Notes
Remember to ask your team about any project-specific setup instructions or tools you might need to install.