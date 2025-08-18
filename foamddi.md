---
layout: default
title: FoamDDI
description: Installers, instructions and documentation for FoamDDI v1.17.8
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

## FoamDDI software overview

FoamDDI units manufactured **before Nov 2020** should use the **legacy 1.7.9** release. Units manufactured **Nov 2020 or later** are generally eligible for the newest release.

---

<style>
  .serial-check { margin: 1rem 0 1rem; padding: 1rem; background:#fff; border-radius:8px; box-shadow:0 3px 8px rgba(0,0,0,0.06); max-width:900px; }
  .serial-row { display:flex; gap:0.5rem; align-items:center; flex-wrap:wrap; margin-top:0.6rem; }
  .serial-row input[type="text"] {
    padding:0.5rem 0.75rem; font-size:1rem; border-radius:6px; border:1px solid #ccc; min-width:220px;
  }
  .serial-row button { padding:0.55rem 0.9rem; border-radius:6px; border:none; cursor:pointer; background:#0073e6; color:#fff; font-weight:600; }
  .serial-result { margin-top:0.75rem; font-size:0.98rem; }
  .ok { color:#065f46; background:#ecfdf5; border:1px solid #d1fae5; padding:0.6rem; border-radius:6px; }
  .no { color:#7f1d1d; background:#fff1f2; border:1px solid #fecaca; padding:0.6rem; border-radius:6px; }
  .links { margin-top:0.6rem; display:flex; gap:0.75rem; flex-wrap:wrap; }
  .links a { text-decoration:none; padding:0.45rem 0.75rem; border-radius:6px; background:#f3f4f6; border:1px solid #e5e7eb; color:#111; }
  .logic-note { margin-top:0.6rem; color:#555; font-size:0.95rem; }
</style>


<div class="serial-check" markdown="0">
  <strong>FoamDDI software compatibility check</strong>

  <div class="serial-row">
    <label for="foam-serial" style="font-weight:500;">Enter serial number found on the back of the unit (first 4 digits or full serial)</label>
    <input id="foam-serial" type="text" placeholder="e.g. 2011 or 20111234" aria-label="FoamDDI serial">
    <button id="foam-check-btn" type="button">Check</button>
  </div>

  <div id="foam-result" class="serial-result" aria-live="polite"></div>

  <div class="links" id="foam-links" style="display:none;">
    <!-- Replace these hrefs with your actual release/asset links -->
    <a id="foam-new" href="https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.17.8/VISAYA.Install.FoamDDI.Complete.1.17.8.0.exe" target="_blank" rel="noopener" style="display:none;">Download new FoamDDI installer</a>
    <a id="foam-legacy" href="https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.7.9/Install.FoamDDI.1.7.9.64bit.exe" target="_blank" rel="noopener" style="display:none;">Download legacy FoamDDI 1.7.9</a>
    <a id="foam-contact" href="mailto:support@visaya.com" style="display:none;">Contact support@visaya.com</a>
  </div>

  <div class="logic-note">
    <strong>Note:</strong> The newest FoamDDI software requires a new tablet-style LogicBox. If you are unsure about your LogicBox, please contact <a href="mailto:support@visaya.com">support@visaya.com</a> before upgrading.
  </div>

  <noscript>
    <div class="serial-result no">JavaScript is disabled — please contact <a href="mailto:support@visaya.com">support@visaya.com</a> with your serial and we will advise.</div>
  </noscript>
</div>

<script>
(function(){
  const btn = document.getElementById('foam-check-btn');
  const inp = document.getElementById('foam-serial');
  const result = document.getElementById('foam-result');
  const linksWrapper = document.getElementById('foam-links');
  const newLink = document.getElementById('foam-new');
  const legacyLink = document.getElementById('foam-legacy');
  const contactLink = document.getElementById('foam-contact');

  function hideAll(){ newLink.style.display='none'; legacyLink.style.display='none'; contactLink.style.display='none'; linksWrapper.style.display='none'; }
  function showOnly(el){ hideAll(); el.style.display='inline-block'; linksWrapper.style.display='flex'; }

  function showMessage(cls, html){
    result.className = 'serial-result ' + cls;
    result.innerHTML = html;
  }

  function check(serialRaw){
    if(!serialRaw){ showMessage('no','Please enter a serial number.'); return; }
    const digits = serialRaw.replace(/\D/g,'');
    if(digits.length < 4){ showMessage('no','Serial too short — enter at least first 4 digits (YYMM).'); return; }
    const prefix = digits.slice(0,4);
    const yy = parseInt(prefix.slice(0,2),10);
    const mm = parseInt(prefix.slice(2,4),10);
    if(isNaN(yy) || isNaN(mm) || mm < 1 || mm > 12){ showMessage('no','Invalid serial prefix: month must be 01–12. Received: ' + prefix); return; }

    const year = 2000 + yy;
    const month = mm;
    const manufactured = year * 100 + month;
    const threshold = 2020 * 100 + 11; // Nov 2020 => 202011

    const monthNames = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
    const friendly = monthNames[month-1] + ' ' + year;

    if(manufactured >= threshold){
      showMessage('ok','<strong>Upgrade OK</strong> — Serial indicates manufacture in <strong>' + friendly + '</strong>.<br>The unit is eligible for the newest FoamDDI software.');
      showOnly(newLink);
    } else {
      showMessage('no',
          '<strong>Use legacy software</strong> — Serial indicates manufacture in <strong>' + friendly + '</strong>.<br>' +
          'Install legacy FoamDDI 1.7.9 for this unit. If you would like to upgrade to a newer unit, please contact <a href="mailto:support@visaya.com">support@visaya.com</a> to discuss options.'
      );
      showOnly(legacyLink);
    }
  }

  btn.addEventListener('click', () => check(inp.value));
  inp.addEventListener('keydown', function(e){ if(e.key === 'Enter'){ e.preventDefault(); check(inp.value); } });

  // auto-check from querystring: ?serial=XXXX
  (function auto(){
    try{
      const params = new URLSearchParams(window.location.search);
      const s = params.get('serial');
      if(s){ inp.value = s; check(s); }
    }catch(e){}
  })();

  hideAll();
})();
</script>


## Installation Steps

1. In the Visaya software go to **Settings → About** and click **Exit Application**.  
2. Log into **VISAYA Admin** using password **`visaya`**.  
3. On each FoamDDI module, power off with the rear on/off switch.  
4. Run the appropriate `*.exe` installer and follow the prompts (defaults are fine).  
5. Power each FoamDDI module back on via its rear switch.  
6. In Windows go to **Start → Power → Restart** to reboot the LogicBox.  
7. After reboot, verify version **1.17.8.0** in **Settings → About**.

---
## Downloads

- **Update‑only installer**  
  [VISAYA Install FoamDDI Update Only 1.17.8](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.17.8/VISAYA.Install.FoamDDI.Update.Only.1.17.8.0.exe)  
- **Full installer**  
  [VISAYA Install FoamDDI Complete 1.17.8](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.17.8/VISAYA.Install.FoamDDI.Complete.1.17.8.0.exe)

#### Legacy Installer 

- **Full installer**  
  [VISAYA Install FoamDDI 1.7.9](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v1.7.9/Install.FoamDDI.1.7.9.64bit.exe)

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
