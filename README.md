# memory-cache-issue
memory-cache-issue

/dev/shm is nothing but implementation of traditional shared memory concept. It is an efficient means of passing data between programs. One program will create a memory portion, which other processes (if permitted) can access. This will result into speeding up things on Linux.


Kernel read and write operations operate on main memory. Whenever any read or write operation is performed, the kernel first needs to copy the required data into memory:

Read operation:
- go to disk and search for data
- write the data from disk into memory
- perform read operation

Write Operation:
- go to disk and search for data
- write the data from disk into memory
- perform write operation
- copy the modified data back to disk

To check and verify cache operation:

cat > XYZ
  hi how r u?
  ^C
  
 sync
 echo 3 > /proc/sys/vm/drop_caches  

time cat XYZ

check before and after cache clear. 

Details: https://access.redhat.com/solutions/67610


The du command, short for "disk usage" reports the estimated amount of disk space used by given files or directories

To find out Cached file size :

git clone  https://github.com/yazgoo/linux-ftools.git
cd linux-ftools/
./configure
make
sudo make install


Usages: 
  linux-fincore --only-cached --pages=false --summarize --only-cached /var/log/messages
  linux-fincore --only-cached --pages=false --summarize --only-cached $(find /var/lib/mysql/ -type f)
  inux-fincore --only-cached --pages=false --summarize --only-cached $(find / -name docker)
  
  
  Cleaning the Page Cache
  sync && \
    echo 1 > /proc/sys/vm/drop_caches && \
    echo 3 > /proc/sys/vm/compact_memory
    
