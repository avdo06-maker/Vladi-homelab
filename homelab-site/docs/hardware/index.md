# Hardware

## Homelab Server

Headless server running **Debian 12 (Bookworm)**, no hypervisor — everything runs as bare-metal services and Docker containers directly on the host.

| Component | Spec |
|---|---|
| Case | Corsair Carbide Series 200R (ATX) |
| CPU | Intel Core i7-6700K @ 4.0 GHz |
| Motherboard | ASRock B150 Pro4S |
| RAM | 4x Samsung DDR4 2400 (16 GB total) |
| GPU | NVIDIA GeForce GTX 1060 (6 GB VRAM) |
| PSU | Thermaltake Smart BM2 750W |
| OS | Debian 12 Bookworm (headless, no hypervisor) |

!!! note "GPU"
    The GTX 1060 is installed but not currently passed through to any container or used for hardware transcoding/AI workloads — update this note if that changes.

### Storage

| Drive Position | Label | Capacity | Manufacturer | Model | Connection |
|---|---|---|---|---|---|
| Top of HDD bay | `win11` (NTFS) / `debian` (ext4) | 931 GB | SanDisk | SSD Plus 1000GB | SATA3_0 |
| HDD Bay 1 | HDD_1 | 3.6 TB | Seagate | ST4000LM024-2AN17V | SATA3_4 |
| HDD Bay 2 | HDD_2 | 3.6 TB | Seagate | ST4000LM024-2AN17V | SATA3_5 |
| HDD Bay 3 | HDD_3 (aka "Expansion") | 5.5 TB | Seagate | ST6000DM003 | SATA3_3 |
| HDD Bay 4 | HDD_Tirol (unlabeled) | 931 GB | Western Digital | WD10EARS | SATA3_1 |

!!! note "Serial numbers omitted"
    Drive serial numbers are tracked in a private inventory, not published here — they're not needed to understand the setup and there's no reason to expose them publicly.

There's also a 256 GB Kyocera NVMe drive attached to the system that's **not** part of the homelab — it's used for testing other OS installs and isn't documented further here.
