---
layout: default
title: Visaya Download Center
description: Downloads and documentation for Visaya’s testing instruments
---

<style>
  /* Tabs fixed at top */
  .tab-nav {
    position: fixed;
    top: 0; left: 0; width: 100%;
    display: flex; gap: 1rem;
    background: #fff; border-bottom: 2px solid #ccc;
    padding: 0.75rem 1rem; z-index: 1000;
  }
  .tab {
    padding: 0.5rem 1rem;
    text-decoration: none; color: #333;
    border: 1px solid transparent; border-bottom: none;
    border-radius: 4px 4px 0 0;
    font-weight: 500;
  }
  .tab:hover { background: #f5f5f5; }
  .tab-active {
    border-color: #ccc; background: #fff; font-weight: 600;
  }

  /* push the theme’s header & content below the tabs */
  header,
  .page-content {
    margin-top: 3.5rem;
  }

  /* Products grid */
  .products {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin: 2rem 0;
  }

  /* Card styles */
  .card {
    background: #fff;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);
    padding: 1.5rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }
  .card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 20px rgba(0,0,0,0.12);
  }
  .card h2 {
    margin-bottom: 1rem;
    font-size: 1.4rem;
    color: #222;
  }
  .card p {
    flex-grow: 1;
    margin-bottom: 1.5rem;
    color: #555;
    line-height: 1.4;
  }
  .card a {
    align-self: start;
    padding: 0.5rem 1rem;
    background: #0073e6;    /* Visaya blue accent */
    color: #fff;
    text-decoration: none;
    border-radius: 4px;
    font-weight: 500;
    transition: background 0.2s ease;
  }
  .card a:hover {
    background: #005bb5;
  }
</style>

<div class="tab-nav" markdown="0">
  <a class="tab tab-active" href="/">Home</a>
  <a class="tab" href="/cuddi/">CuDDI</a>
  <a class="tab" href="/foamddi/">FoamDDI</a>
</div>



# Visaya Download Center

Welcome—here you’ll find installers, updates, and documentation for our core Visaya instruments. Click on a card to get started.

<div class="products" markdown="0">

  <div class="card">
    <h2>CuDDI</h2>
    <p>Automated copper corrosion detection system (ASTM D130, D1838).</p>
    <a href="/cuddi/">Go to CuDDI</a>
  </div>

  <div class="card">
    <h2>FoamDDI</h2>
    <p>Foaming‑characteristics tester for oil and coolant standards (ASTM D892, D6082).</p>
    <a href="/foamddi/">Go to FoamDDI</a>
  </div>

</div>

<p style="text-align:center; color:#888; font-size:0.9rem;">
  © {{ site.time | date: "%Y" }} Visaya Engineering
</p>


