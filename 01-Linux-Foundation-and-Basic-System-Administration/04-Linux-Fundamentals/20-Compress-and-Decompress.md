# Archiving & Compression in Linux — `tar`, `gzip`, `gunzip`

I learned how to:

- Combine multiple files into one container
- Compress files to reduce size
- Extract and uncompress files

These skills are **extremely important** in:
- System administration
- Log transfers
- Backups
- Incident response
- Sending files to support teams

---

# Why Do We Need `tar` and `gzip`?

### Real-World Scenario

Your Linux server crashes.

You:
- Check logs
- Troubleshoot
- Try to fix it

Nothing works.

You call Red Hat support.

They say:
> "Send us all logs from `/var/log`."

Now you have:
- Hundreds of files
- Subdirectories
- Large file sizes

Are you going to send them one by one?

❌ No.

Instead:
1. Combine everything into one file → `tar`
2. Compress that file → `gzip`
3. Send one small file

That’s the power of archiving + compression.

---

# 1️⃣ `tar` — Archive Files (Container)

## Important

`tar` DOES NOT compress by default.

It:
- Collects files
- Packages them
- Creates a single container file

Think of it like:
> Putting many files into one box.

---

# Create a Tar Archive

## Syntax

    tar -cvf archive-name.tar files-or-directories

### Meaning of options:

| Option | Meaning |
|--------|----------|
| `-c` | Create archive |
| `-v` | Verbose (show progress) |
| `-f` | File name |

---

## Example: Archive Entire Home Directory

From inside your home directory:

    tar -cvf backup.tar .

`.` means:
> Everything in the current directory

Now check:

    ls -ltr

You will see:

    backup.tar

---

# Extract (Untar) Files

To extract:

    tar -xvf backup.tar

| Option | Meaning |
|--------|----------|
| `-x` | Extract |
| `-v` | Verbose |
| `-f` | File |

Files will be extracted in current directory.

---

# Extract to Different Directory

Create folder:

    mkdir restore

Move archive:

    mv backup.tar restore

Go inside:

    cd restore

Extract:

    tar -xvf backup.tar

Now contents appear inside `restore`.

---

# 2️⃣ `gzip` — Compress Files

`gzip` reduces file size.

It works on:
- Single files
- Tar archives
- Logs

---

## Compress a File

    gzip backup.tar

This creates:

    backup.tar.gz

Original `.tar` file is removed.

---

## Check Size Before and After

Before:

    ls -lh backup.tar

After:

    ls -lh backup.tar.gz

You’ll see:
- Size significantly reduced

---

# Uncompress (`gunzip`)

To reverse compression:

    gunzip backup.tar.gz

OR

    gzip -d backup.tar.gz

This restores:

    backup.tar

---

# Full Workflow (Professional Method)

In real environments, we usually combine tar + gzip:

    tar -cvzf backup.tar.gz .

| Option | Meaning |
|--------|----------|
| `-z` | Compress with gzip |
| `-c` | Create |
| `-v` | Verbose |
| `-f` | File name |

This:
- Archives
- Compresses
- Creates `.tar.gz` in one step

---

# Extract `.tar.gz`

    tar -xvzf backup.tar.gz

This:
- Uncompresses
- Extracts

In one command.

---

# Summary of Commands

| Task | Command |
|------|----------|
| Create tar | `tar -cvf file.tar dir/` |
| Extract tar | `tar -xvf file.tar` |
| Compress | `gzip file.tar` |
| Uncompress | `gunzip file.tar.gz` |
| Tar + gzip | `tar -cvzf file.tar.gz dir/` |
| Extract tar.gz | `tar -xvzf file.tar.gz` |

---

# When to Use What?

| Situation | Command |
|------------|----------|
| Send many logs | `tar` |
| Reduce file size | `gzip` |
| Send support bundle | `tar + gzip` |
| Backup config files | `tar -cvzf` |
| Restore backup | `tar -xvzf` |

---

# Security & SOC Use Cases

- Collect logs for investigation
- Archive compromised system snapshot
- Send evidence to forensic team
- Create compressed backups
- Deploy software packages

---

# Important Notes

- `tar` = container
- `gzip` = compression
- `.tar.gz` = compressed archive
- Always check size before transfer
- Use `-z` to combine tar + gzip

---

# Final Thought

Mastering `tar` and `gzip` gives you:

- Efficient file management
- Faster file transfers
- Better backup strategy
- Stronger Linux troubleshooting skills

These commands are heavily used in:
- Production servers
- Cloud systems
- Security operations
- DevOps environments

Practice:
- Archive your home directory
- Compress it
- Extract it
- Verify integrity

That’s how you build confidence.

---

**✍️ Notes By Abhishek (Ez Abyss)**  
