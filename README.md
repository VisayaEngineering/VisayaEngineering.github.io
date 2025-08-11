## How to update Software and Firmware for website with Releases


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





### Welcome to GitHub Pages
You can use the [editor on GitHub](https://github.com/VisayaEngineering/VisayaEngineering.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [Basic writing and formatting syntax](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/VisayaEngineering/VisayaEngineering.github.io/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
