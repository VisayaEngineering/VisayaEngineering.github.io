---
layout: default
title: FoamDDI
description: Installers, instructions and documentation for FoamDDI v1.17.7
permalink: /foamddi/
---


<style>
  .tab-nav {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    display: flex;
    gap: 1rem;
    background: #fff;
    border-bottom: 2px solid #ccc;
    padding: 0.5rem 1rem;
    z-index: 1000;
  }
  .tab {
    padding: 0.5rem 1rem;
    text-decoration: none;
    color: inherit;
    border: 1px solid transparent;
    border-bottom: none;
    border-radius: 4px 4px 0 0;
  }
  .tab:hover { background: #f5f5f5; }
  .tab-active {
    border-color: #ccc;
    background: #fff;
    font-weight: bold;
  }

   header {
    margin-top: 3.5rem; /* adjust this until nothing overlaps */
  }
</style>

<div class="tab-nav" markdown="0">
  <a class="tab" href="/">Home</a>
  <a class="tab" href="/cuddi/">CuDDI</a>
  <a class="tab tab-active" href="/foamddi/">FoamDDI</a>
  …
</div>

## Installation Steps

1. In the Visaya software go to **Settings → About** and click **Exit Application**.  
2. Log into **VISAYA Admin** using password **`visaya`**.  
3. On each FoamDDI module, power off with the rear on/off switch.  
4. Run the appropriate `*.exe` installer and follow the prompts (defaults are fine).  
5. Power each FoamDDI module back on via its rear switch.  
6. In Windows go to **Start → Power → Restart** to reboot the LogicBox.  
7. After reboot, verify version **1.17.7.0** in **Settings → About**.

---
## Downloads

- **Update‑only installer**  
  [VISAYA Install FoamDDI Update Only 1.17.7](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.17.7/VISAYA_Install_FoamDDI_Update_Only_1.17.7.0.4.exe)  
- **Full installer**  
  [VISAYA Install FoamDDI Complete 1.17.7](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.17.7/VISAYA_Install_FoamDDI_Complete_1.17.7.0.1.exe)

---
## Post‑Update Connectivity

If modules still fail to connect:

- Power off the module for **30 seconds**.  
- Inspect and reseat the USB cable.  
- Power back on and allow the Visaya software up to **2 minutes** to reconnect.  
- If it still doesn’t appear, restart the Visaya application.

---

## Camera Firmware Update

Some Gen 2 modules will prompt for a camera‑firmware update after installing the software. To update:

1. Download the firmware bundle:  
   [Alvium_U3V_Camera_00.14.00.baba1e3c.avf](../assets/downloads/Alvium_U3V_Camera_00.14.00.baba1e3c.avf)  
2. Open **Upgrading Camera Firmware.pdf** (below) for step‑by‑step instructions.  
3. Apply the update to **both** cameras on each module.

---

## Additional Documentation

- [Upgrading Camera Firmware.pdf](../assets/docs/Updating_Camera_Firmware.pdf)  
- [FoamDDI Ver 2 – User Manual (R1.8)](../assets/docs/FoamDDI_User_Manual_R1.8.pdf)  
- [FoamDDI Software Release Bulletin 1.17](../assets/docs/VISAYA_FoamDDI_Software_Release_Bulletin_1.17.pdf)
- [FoamDDI Software Release Bulletin 1.16](../assets/docs/VISAYA_FoamDDI_Software_Release_Bulletin_1.16.pdf)

---

## Support  
For maintenance and troubleshooting, email support@visaya.com.  
