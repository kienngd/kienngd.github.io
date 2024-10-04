# How to Use ZRAM on Ubuntu 24.04


# How to Use ZRAM on Ubuntu 24.04

## What is ZRAM?

ZRAM is a Linux kernel module. It creates a compressed block device in RAM. This block device can be used for swap space or as a temporary filesystem. Because it is compressed, it saves memory and can make your system faster.

## Pros and Cons of Using ZRAM

**Pros:**
1. **Faster Swap**: ZRAM is much faster than a traditional swap on a hard disk.
2. **Better Performance**: It can improve performance by reducing I/O on slower disks.
3. **More Efficient Memory Use**: It compresses data, so you can store more in RAM.

**Cons:**
1. **CPU Usage**: Compression and decompression use CPU resources.
2. **Limited Space**: The size of ZRAM is limited to the amount of RAM you have.

## How to Use ZRAM on Ubuntu 24.04

1. **Install ZRAM Tools**:

   Open a terminal and type
   ```bash
   sudo apt update
   sudo apt install zram-tools
   ```

2. **Configure ZRAM**:

   Create or edit the configuration file
   ```bash
   sudo nano /etc/default/zramswap
   ```
   Add or modify the following lines:
   ```bash
   ENABLED=true
   ALGO=zstd
   PERCENTAGE=50
   PRIORITY=100
   ```
   Here, `PERCENTAGE=50` means ZRAM will use 50% of your total RAM.

3. **Enable ZRAM**:

   Start and enable the ZRAM service
   ```bash
   sudo systemctl enable zramswap
   sudo systemctl start zramswap
   ```

4. **Verify ZRAM**:

   Check if ZRAM is running
   ```bash
   sudo zramctl
   ```
   You should see an output showing the ZRAM device(s).

## How Much RAM to Use for ZRAM

Using 50% of your RAM for ZRAM is a good starting point. This works well for most systems. If you have 8GB of RAM, ZRAM will use 4GB. Adjust the percentage based on your needs. If your system often runs out of memory, you might use a higher percentage. If your CPU is slow, use a lower percentage to reduce the load.

## Summary

ZRAM can make your Ubuntu server faster by using compressed swap space in RAM. It is easy to set up and can improve performance, especially on systems with limited memory or slow disks. Start with 50% of your RAM for ZRAM and adjust as needed.
