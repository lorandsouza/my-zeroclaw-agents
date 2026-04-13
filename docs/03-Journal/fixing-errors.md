#  Debugging Journal — Nova Agent Build

> Building Nova was not just about creating an agent —  
> it was about understanding how systems fail, and how to fix them.

---

##  Problem 1: Server Creation Failure

###  Issue
Attempting to provision a server resulted in:
> *"Failed to rent server: Primary IP limit exceed"*

---

###  Investigation
- Deleted existing (ghost) server instances
- Switched geographic regions
- Retried multiple times

---

###  Root Cause
Temporary infrastructure or quota limitation from the cloud provider.

---

###  Resolution
- Waited ~2 hours
- Retried server creation → succeeded

---

##  Problem 2: file_write Permission Denied

###  Issue
Telegram agent returned:
> *"Hmm, it seems the file write was denied"*

---

###  Root Cause
The `file_write` tool was not authorised in the ZeroClaw configuration.

---

### Fix

Updated:

~/.zeroclaw/config.toml

Added:

```toml
[autonomy]
auto_approve = ["file_write"]

Restarted daemon:

ps aux | grep zeroclaw
kill <process_id>
zeroclaw daemon

##  Problem 3: Files Not Created Despite Success Message

###  Issue
The agent confirmed that files were successfully created, but no files existed in the directory.

###  Investigation
Checked directory:
```bash
ls -R ~/.zeroclaw/workspace/nova

Tested manual write:

echo "test" > test.txt. Filesystem worked correctly

### Root Cause
- Agent hallucinated successful execution
- file_write tool calls were incorrectly formatted

### Fix
Stopped relying on agent confirmation. 
Double checked every time it confirmed that it's done

## Problem 4: Incorrect Path Handling (~ symbol)

### Issue

Agent failed to write files when using:
~/.zeroclaw/workspace/nova/

### Root Cause

Agents do not interpret ~ (home directory shorthand) like a Linux shell.

### Fix

Used absolute path instead:

/root/.zeroclaw/workspace/nova/

## Problem 5: YouTube Processing Issues
### Issue
Video processing failed or produced unreliable results
Agent claimed completion without verifiable output
### Root Cause
VPN/network restrictions blocking access
External API limitations
Agent hallucination
### Fix
Switched to Apify YouTube API
Verified outputs manually before trusting results

### Key Learnings
- Never trust agent output without verification
- Always validate system state using terminal commands
- Use absolute paths when working with agents
- Tool execution must be confirmed, not assumed
- External APIs introduce real-world failure points
- Debugging is more valuable than initial success