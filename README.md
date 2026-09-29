# IFW Absolute Zero 

A thermodynamic approach to Android system-level ad blocking. By shifting the defensive matrix from application memory (Ring 3) and network routing (Ring 0) to the Android Framework layer (Ring 1), this module achieves absolute ad-component eradication without triggering commercial anti-tamper mechanisms.

## First Principles Analysis

Traditional ad-blocking solutions operate on fundamentally flawed topologies when dealing with heavily fortified commercial applications (e.g., banking apps, carrier apps, enterprise cloud drives):
1. **Ring 3 Hooking (LSPosed/Zygisk):** Injecting code into Dalvik/ART virtual machines alters the stack trace and triggers native Watchdog self-destruction (crashes).
2. **Ring 0 Routing (Iptables/DNS):** Blocking DoH (DNS over HTTPS) or standard port 53 alters the TCP fingerprint, conflicting with transparent proxy engines (like Mihomo/Sing-box) and triggering network risk-control systems.

**The Solution:**
This module abandons network and memory interference entirely. It utilizes Android's native **Intent Firewall (IFW)**. When an ad SDK attempts to request rendering resources from the ActivityManagerService (AMS), the IFW acts as a rigid physical barrier, silently dropping the IPC request. 

The ad data becomes "dark matter" in the memory pool—it exists, but mathematically cannot be rendered to the screen. The host application assumes a standard system interruption and gracefully degrades to the main UI without crashing.

## Architectural Topology

* **Zero Network Entropy:** Does not modify `hosts`, `iptables`, or proxy routing rules. Your L4 TCP/TLS fingerprints remain 100% native.
* **Absolute Anti-Tamper Bypass:** Does not inject into the target app's memory space. Watchdogs and integrity checks remain dormant.
* **Zero Compute Overhead:** Relies entirely on the native `system_server` IPC rejection mechanism. No GPU rendering cycles or CPU wait-states are wasted on ad components.

## Target Matrix

The current XML matrix neutralizes the component instantiation of the following commercial SDKs:
* **ByteDance Pangle (穿山甲联盟)**
* **Tencent GDT (广点通/优量汇)**
* **Baidu MobAds (百度百青藤)**
* **Kuaishou Union (快手联盟)**
* **Sigmob / Mintegral**

## Deployment

**Requirements:** KernelSU or Magisk (Root access is required for initial `/data/system/ifw` topological injection).

1. Download the latest `IFW-Absolute-Zero.zip` from the Releases page.
2. Flash the module via KernelSU or Magisk.
3. (Optional) Perform a soft reboot (`reboot zygote`) or full reboot to force AMS state synchronization.
4. Remove any legacy Xposed/LSPosed ad-blocking modules targeting the same apps to prevent structural conflicts.

## Disclaimer

This project strictly manipulates local Android OS component routing tables. It does not reverse-engineer, decrypt, or distribute any proprietary commercial SDK code.
