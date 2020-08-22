# SR-IOV NIC Passthrough
Direct NIC assignment allows a virtual mahcine to have an exclusive access to the device and achieve the near-native network performance.

# Network Card
Mellanox ConnectX-3 Pro (MLX)

# Network Layout
<img src="iperf.png" width="50%" height="50%">

# Set Up a Virtual Function
```
modprobe -r mlx4_ib
modprobe -r mlx4_en
modprobe -r mlx4_core
vfs=1
modprobe mlx4_core num_vfs=$vfs log_num_mgm_entry_size=-1 port_type_array=2,2
```

# Set Up a Private Network on MLX
- d12
```
ip link set ens4 up
ip addr add 192.168.0.12/24 dev ens4
```
- d13
```
ip link set ens4 up
ip addr add 192.168.0.13/24 dev ens4
```
- test on d12
```
ping -c 1 -w 1 192.168.0.13
```
