🔹 Check memory usage before clearing:
free -h

🔹 Clear PageCache only:
sudo sync; echo 1 | sudo tee /proc/sys/vm/drop_caches

🔹 Clear dentries and inodes:
sudo sync; echo 2 | sudo tee /proc/sys/vm/drop_caches

🔹 Clear PageCache + dentries + inodes (all caches):
sudo sync; echo 3 | sudo tee /proc/sys/vm/drop_caches
