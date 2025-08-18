---
layout: default
title: CuDDI
permalink: /cuddi/
description: Installers and documentation for CuDDI v3.0.8.0
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

<!-- Serial compatibility checker -->
<style>
  .serial-check {
    margin: 1rem 0 1.5rem;
    padding: 1rem;
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 3px 8px rgba(0,0,0,0.06);
    max-width: 900px;
  }
  .serial-row { display:flex; gap:0.5rem; align-items:center; flex-wrap:wrap; }
  .serial-row input[type="text"]{
    padding:0.5rem 0.75rem; font-size:1rem; border-radius:6px; border:1px solid #ccc; min-width:200px;
  }
  .serial-row button {
    padding:0.55rem 0.9rem; border-radius:6px; border:none; cursor:pointer;
    background:#0073e6; color:#fff; font-weight:600;
  }
  .serial-result { margin-top:0.75rem; font-size:0.98rem; }
  .ok { color: #065f46; background: #ecfdf5; border: 1px solid #d1fae5; padding:0.6rem; border-radius:6px; }
  .warn { color: #92400e; background: #fff7ed; border:1px solid #ffedd5; padding:0.6rem; border-radius:6px; }
  .no { color:#7f1d1d; background:#fff1f2; border:1px solid #fecaca; padding:0.6rem; border-radius:6px; }
  .serial-hint { color:#666; font-size:0.9rem; margin-top:0.5rem; }
  .links { margin-top:0.6rem; display:flex; gap:0.75rem; flex-wrap:wrap; }
  .links a { text-decoration:none; padding:0.45rem 0.75rem; border-radius:6px; background:#f3f4f6; border:1px solid #e5e7eb; color:#111; }
</style>

<div class="tab-nav" markdown="0">
  <a class="tab" href="/">Home</a>
  <a class="tab tab-active" href="/cuddi/">CuDDI</a>
  <a class="tab" href="/foamddi/">FoamDDI</a>


  …
</div>

## CuDDI software overview

We publish two tracks — the **new (v3.x)** release with the latest features (requires newer camera hardware), and the **legacy (v2.x)** release for older Basler-camera units. Use the compatibility checker below to get an immediate recommendation: **Upgrade**, **Contact support**, or **Stay on legacy**.

We are actively working to make the new software available for all units; if your unit isn't yet eligible and you'd like it to be, please contact **support@visaya.com** and we'll advise on next steps.



---


<div class="serial-check" markdown="0">
  <strong>CuDDI software compatibility check</strong>

  <div class="serial-row" style="margin-top:.6rem;">
    <label for="serial" style="font-weight:500;">Enter serial number found on the back of the unit (first 4 digits or full serial):</label>
    <input id="serial" type="text" placeholder="e.g. 2011 or 20111234" aria-label="CuDDI serial number">
    <button id="serial-check-btn" type="button">Check</button>
  </div>

  <div id="serial-result" class="serial-result" aria-live="polite"></div>


  <div class="links" id="serial-links" style="display:none;">

  <!-- New installer (shown only for "Upgrade OK") -->
  <a id="new-installer"
     href="https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v3.0.8.0/VISAYA.Install.CuDDI.Complete.3.0.8.0.exe"
     target="_blank" rel="noopener"
     style="display:none;">Download new CuDDI installer</a>

  <!-- Legacy installer (shown only for "Do NOT upgrade") -->
  <a id="old-installer"
     href="https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v2.2.9.0/VISAYA.Install.CuDDI.Complete.2.2.9.0.exe"
     target="_blank" rel="noopener"
     style="display:none;">Download legacy CuDDI installer</a>

  <!-- Contact (shown only for "Possible compatibility issue") -->
  <a id="contact-link"
     href="mailto:support@visaya.com"
     style="display:none;">Contact support@visaya.com</a>
</div>

  <noscript>
    <div class="serial-result warn">JavaScript is disabled — please contact <a href="mailto:support@visaya.com">support@visaya.com</a> with your serial and we will advise.</div>
  </noscript>
</div>




<script>
(function(){
  const btn = document.getElementById('serial-check-btn');
  const inp = document.getElementById('serial');
  const result = document.getElementById('serial-result');
  const linksWrapper = document.getElementById('serial-links');

  // link elements
  const newLink = document.getElementById('new-installer');
  const oldLink = document.getElementById('old-installer');
  const contactLink = document.getElementById('contact-link');

  function hideAllLinks(){
    newLink.style.display = 'none';
    oldLink.style.display = 'none';
    contactLink.style.display = 'none';
    linksWrapper.style.display = 'none';
  }

  function showOnly(linkElement){
    hideAllLinks();
    linkElement.style.display = 'inline-block';
    linksWrapper.style.display = 'flex';
  }

  function showMessage(type, html){
    result.className = 'serial-result ' + type;
    result.innerHTML = html;

    if(type === 'ok'){
      showOnly(newLink);
    } else if(type === 'warn'){
      showOnly(contactLink);
    } else if(type === 'no'){
      showOnly(oldLink);
    } else {
      hideAllLinks();
    }
  }

  function parseAndCheck(raw){
    if(!raw) { showMessage('warn','Please enter a serial number.'); return; }
    const digits = raw.replace(/\D/g,'');
    if(digits.length < 4){ showMessage('no','Serial too short — enter at least the first 4 digits (YYMM).'); return; }
    const prefix = digits.slice(0,4);
    const yy = parseInt(prefix.slice(0,2),10);
    const mm = parseInt(prefix.slice(2,4),10);

    if(isNaN(yy) || isNaN(mm) || mm < 1 || mm > 12){
      showMessage('no','Invalid serial prefix: month must be 01–12. Received: ' + prefix);
      return;
    }

    const year = 2000 + yy;
    const month = mm;
    const manufactured = year * 100 + month;
    const thresholdUpgrade = 2024 * 100 + 8; // Aug 2024
    const threshContactFrom = 2023 * 100 + 1; // Jan 2023

    const monthNames = ['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec'];
    const friendly = monthNames[month-1] + ' ' + year;

    if(manufactured >= thresholdUpgrade){
      showMessage('ok',
        '<strong>Upgrade OK</strong> — Serial indicates manufacture in <strong>' + friendly + '</strong>.<br>' +
        'This unit is compatible with the new CuDDI software.'
      );
    } else if(manufactured >= threshContactFrom && manufactured < thresholdUpgrade){
      showMessage('warn',
        '<strong>Possible compatibility issue</strong> — Serial indicates manufacture in <strong>' + friendly + '</strong>.<br>' +
        'Please contact support for a quick verification before upgrading.'
      );
    } else {
      showMessage('no',
        '<strong>Do NOT upgrade</strong> — Serial indicates manufacture in <strong>' + friendly + '</strong>.<br>' +
        'This unit uses the older Basler camera and must stay on the legacy software.'
      );
    }
  }

  btn.addEventListener('click', function(){ parseAndCheck(inp.value); });
  inp.addEventListener('keydown', function(e){
    if(e.key === 'Enter'){ e.preventDefault(); parseAndCheck(inp.value); }
  });

  // prefill from ?serial= query parameter if present
  (function checkQueryString(){
    try {
      const params = new URLSearchParams(window.location.search);
      const s = params.get('serial');
      if(s){
        inp.value = s;
        parseAndCheck(s);
      }
    } catch(e){}
  })();

  // initialize hidden
  hideAllLinks();
})();
</script>




## Installation Steps

1. In the Visaya software go to **Settings → About**, then click **Exit Application**.  
2. Log into **VISAYA Admin** using password **`visaya`**.  
3. Run the appropriate `*.exe` installer and follow the prompts (defaults are fine).  
4. In Windows go to **Start → Power → Restart** to reboot the LogicBox.  
5. After reboot, verify version **3.0.8.0** in **Settings → About**.

---
## Downloads

- **Update‑only installer**  
  [VISAYA Install CuDDI Update Only 3.0.8.0](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v3.0.8.0/VISAYA.Install.CuDDI.Update.Only.3.0.8.0.exe)  
- **Full installer**  
  [VISAYA Install CuDDI Complete 3.0.8.0](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v3.0.8.0/VISAYA.Install.CuDDI.Complete.3.0.8.0.exe)

#### Legacy Installer (for older Basler cameras)

- **Update‑only installer**  
  [VISAYA Install CuDDI Update Only 2.2.9.0](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v2.2.9.0/VISAYA.Install.CuDDI.Update.Only.2.2.9.0.exe)  
- **Full installer**  
  [VISAYA Install CuDDI Complete 2.2.9.0](https://github.com/VisayaEngineering/VisayaEngineering.github.io/releases/download/v2.2.9.0/VISAYA.Install.CuDDI.Complete.2.2.9.0.exe) 
  

---

## Documentation

- [CuDDI – User Manual (Rev 3.0)](../assets/docs/CuDDI_User_Manual_SF3.0_High_Res.pdf)

---

## Support  
For maintenance and troubleshooting, email support@visaya.com.  