## How to update Software downloads for website with Releases


1. In the repo, click “**Releases**” (on the right side) → “Draft a new release”.

2. In Tag version, create a new version tag (`v1.17.7`).

3. **Release title**: e.g. “FoamDDI Software v1.17.7”.

4. Under “**Attach binaries by dropping them here or selecting them**”, drag in both `.exe` files (the update‐only and the complete installer).

5. Wait for GitHub to finish uploading—you’ll see them listed under “**Binary assets**”.

6. Click “**Publish release**”.

7. After publishing, each asset has a Download link.

8. Right‑click the links and choose “**Copy link address**”. It will look like:
   `https://github.com/<your‑username>/<repo‑name>/releases/download/v1.17.7/VISAYA_Install_FoamDDI_Update_Only_1.17.7.0.exe`

9. Update the links in the appropriate Markdown files (e.g. `cuddi.md`, `foamddi.md`) in the repo, replacing the old version numbers with the new ones.


Don't forget to update the version number in the file name as well! The Title and in the Installation Steps section.





