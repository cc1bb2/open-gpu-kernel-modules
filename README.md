# NVIDIA driver 570.148.08-p2p with GPUDirect RDMA for 4080

This allows using GDR on AD10x (RTX 40xx / Ada Lovelace) GPUs with the 570.148.08-p2p driver version.

## How to Build

1) Install https://docs.nvidia.com/datacenter/tesla/tesla-release-notes-570-148-08/index.html
2) Run `./install.sh`
3) Reboot


## Sample ib_write_bw output:

```
./ib_write_bw -d mlx5_0 --use_cuda=0
```

```

Perftest doesn't supports CUDA tests with inline messages: inline size set to 0

************************************
* Waiting for client to connect... *
************************************
initializing CUDA
Listing all CUDA devices in system:
CUDA device 0: PCIe address is 10:00

Picking device No. 0
[pid = 5323, dev = 0] device name = [NVIDIA GeForce RTX 4080]
creating CUDA Ctx
making it the current CUDA Ctx
CUDA device integrated: 0
allocated GPU buffer of a 131072 address at 0x5af3874d4fb0 for type CUDA_MEM_DEVICE
---------------------------------------------------------------------------------------
                    RDMA_Write BW Test
 Dual-port       : OFF          Device         : mlx5_0
 Number of qps   : 1            Transport type : IB
 Connection type : RC           Using SRQ      : OFF
 PCIe relax order: ON           Lock-free      : OFF
 ibv_wr* API     : ON           Using Enhanced Reorder      : OFF
 CQ Moderation   : 1
 CQE Poll Batch  : Dynamic
 Mtu             : 4096[B]
 Link type       : IB
 Max inline data : 0[B]
 rdma_cm QPs     : OFF
 Data ex. method : Ethernet
---------------------------------------------------------------------------------------
 local address: LID 0x01 QPN 0x0066 PSN 0xdcb546 RKey 0x1fffbd VAddr 0x007255bb410000
 remote address: LID 0x01 QPN 0x0067 PSN 0xfd3206 RKey 0x2000be VAddr 0x007e0751410000
---------------------------------------------------------------------------------------
 #bytes     #iterations    BW peak[MiB/sec]    BW average[MiB/sec]   MsgRate[Mpps]
 65536      5000             14954.91            14948.67                    0.239179
---------------------------------------------------------------------------------------
deallocating GPU buffer 00007255bb400000
destroying current CUDA Ctx
```
