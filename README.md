# BPQ_7plus

BPQ Mail 7plus Find & Decode Linux Scripts, adapted for use on a Raspberry Pi running LinBPQ from the [Hibbian](https://www.hibbian.org) repository.

## Files

- **`find_7p.sh`**  
  Finds 7plus parts in any new messages since the last run.

- **`7p_decode.sh`**  
  Decodes any parts found by `find_7p.sh`, based on its log file.

- **`7plus`**  
  Executable for Raspberry Pi OS to decode 7p files.

- **`index.html`**  
  Copy this file to `/opt/oarc/bpq/HTML/7plus/index.html` to display decoded files via the web UI.

## Setup Instructions

### 1. Clone the Repository

Clone the repository to the LinBPQ basedir:

```bash
cd /opt/oarc/bpq
git clone https://github.com/gm5dna/BPQ_7plus
cd BPQ_7plus
```

### 2. Edit the Scripts

Modify the scripts as needed:

```bash
nano find_7p.sh
```

```bash
nano 7p_decode.sh
```

### 3. Make the Scripts Executable

Ensure that the scripts are executable:

```bash
sudo chmod +x find_7p.sh
sudo chmod +x 7p_decode.sh
```

### 4. Create Required Directories

Ensure the directory `bpq/HTML/7plus` exists, as the scripts will place decoded files here:

```bash
cd /opt/oarc/bpq/HTML/
mkdir 7plus
```

### 5. Copy `index.html` to the Appropriate Directory

Copy the `index.html` file to `/opt/oarc/bpq/HTML/7plus/`:

```bash
cp /opt/oarc/bpq/BPQ_7plus/index.html /opt/oarc/bpq/HTML/7plus/
```

### 6. Test the Scripts

Test the scripts to ensure they're working:

```bash
cd /opt/oarc/bpq/BPQ_7plus/
./find_7p.sh
./7p_decode.sh
```

### 7. Set Up Cron Jobs

Schedule the scripts to run periodically by editing your crontab:

```bash
crontab -e
```

Add the following lines to your crontab:

```bash
# Find 7plus parts
0 * * * * /opt/oarc/bpq/BPQ_7plus/find_7p.sh

# Reassemble them
0 * * * * /opt/oarc/bpq/BPQ_7plus/7p_decode.sh
```

## Notes

### 1. Configure the `latest_mailfile`

- On its first run, the script creates a file named `latest_mailfile` with a default value of `0`.
- To avoid processing all messages, you can manually create this file with a starting message number, e.g.: `3187`

### 2. Web Interface

- The decoded files are listed in the `bpq/HTML/7plus` directory.
- A `list.csv` file is automatically generated to index the files in this directory.
- The `index.html` file uses `list.csv` to display the decoded files when you visit the web UI:  

  [http://127.0.0.1:8080/7plus/index.html](http://127.0.0.1:8080/7plus/index.html)
