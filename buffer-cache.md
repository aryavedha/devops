🔹 Check memory usage before clearing:
```
free -h
```
🔹 Clear PageCache only:
```
sudo sync; echo 1 | sudo tee /proc/sys/vm/drop_caches
```
🔹 Clear dentries and inodes:
```
sudo sync; echo 2 | sudo tee /proc/sys/vm/drop_caches
```

🔹 Clear PageCache + dentries + inodes (all caches):
```
sudo sync; echo 3 | sudo tee /proc/sys/vm/drop_caches
```
---
- buffer & cache script(80% usage-autoclean)
📝 Script: auto-clear-cache.sh
```
#!/bin/bash
# =====================================================
# Auto Clear Buffer & Cache when memory > 80%
# Author: Arya Vedha
# =====================================================

THRESHOLD=80

# Get current memory usage %
MEM_USED=$(free | awk '/Mem:/ {printf("%.0f", $3/$2 * 100)}')

if [ "$MEM_USED" -ge "$THRESHOLD" ]; then
    echo "[ALERT] Memory usage is at ${MEM_USED}% (>=${THRESHOLD}%)."
    echo "[INFO] Flushing filesystem buffers..."
    sync
    echo 3 | sudo tee /proc/sys/vm/drop_caches > /dev/null
    echo "[INFO] Clearing swap memory..."
    sudo swapoff -a && sudo swapon -a
    echo "[INFO] Cache cleared ✅"
else
    echo "[INFO] Memory usage is at ${MEM_USED}%. No cleanup needed."
fi
```

🔧 Usage
```
Save as auto-clear-cache.sh
```
Make it executable:
```
chmod +x auto-clear-cache.sh
```

Run manually to test:
```
./auto-clear-cache.sh
```
⏲ Automating with Cron

Add this script to cron so it checks every 5 minutes:
```
crontab -e
```

Add:
```
*/5 * * * * /path/to/auto-clear-cache.sh >> /var/log/auto-clear-cache.log 2>&1
```
⚡ Alternative (systemd timer for better control)

If you prefer systemd, create a service:
```
/etc/systemd/system/auto-clear-cache.service
```
[Unit]
```
Description=Auto Clear Cache when memory > 80%
```
[Service]
```
ExecStart=/path/to/auto-clear-cache.sh


/etc/systemd/system/auto-clear-cache.timer
```

[Unit]
```
Description=Run auto-clear-cache script every 5 minutes
```

[Timer]
```
OnUnitActiveSec=5min
Unit=auto-clear-cache.service
```

[Install]
```
WantedBy=timers.target
```

Enable it:
```
sudo systemctl daemon-reexec
sudo systemctl enable --now auto-clear-cache.timer
```
