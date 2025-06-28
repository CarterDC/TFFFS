# **T**utorials **F**or my **F**uture **F**orgetful **S**elf

Mostly testing mkdocs + material to write personal guides about home server set up ( *in order not to have to re-discover the wheel every few years when it's time re-install* ).

---

## Content



---

## Material for Mkdocs 
Some documentation about the documentation system itself.  
TODO : move to own file at some point, along with cheat_sheet ? 
### Links
* [Personnal Cheat Sheet](cheat_sheet.md) *Syntax examples* 
* [Markdown Documentation](https://python-markdown.github.io/extensions/)
* [Material Documentation](https://squidfunk.github.io/mkdocs-material/reference/)
* [James Willet's Tutorial](https://jameswillett.dev/getting-started-with-material-for-mkdocs/#introduction) *(includes github actions for auto publish on project pages)*

### Project layout

    mkdocs/            # Project Folder
    ├── .github
    │   └── worflows
    │       └── ci.yml # Continuous Integration : auto-deploy to GitHub Pages on push request
    ├── docs/
    │   ├── styles/
    │   │   └── extra.css
    │   ├── index.md   # This page
    │   ├── cheat_sheet.md
    │   └── ... 
    ├── .gitignore     # /!\ don't include .github/workflow in the ignore list !!!
    └── mkdocs.yml

### Current yaml
``` yaml title="yaml"
site_name: Doc perso
theme:
  name: material
  logo: assets/lemur.jpg
  font:
    text: Inter
    code: Fira Code
  icon:
    annotation: material/information
  palette:
    # Dark Mode
    - scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Dark mode
      primary: indigo
      accent: amber

    # Light Mode
    - scheme: default
      toggle:
        icon: material/weather-night
        name: Light mode
      primary: blue
      accent: deep orange
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.top
    #- toc.integrate
    - content.code.annotate
    - content.code.copy
extra_css:
  - styles/extra.css # actually located in docs/styles/
markdown_extensions:
  - attr_list
  - md_in_html
  - admonition
  - pymdownx.details      
  - pymdownx.superfences  
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - pymdownx.snippets

  #- pymdownx.snippets:
  #    auto_append:
  #      - includes/abbreviations.md

nav:
  - Home: index.md
  - Home Server Setup:
    - Intro: homeserver/index.md
    - SSH: homeserver/ssh.md
    - Samba: homeserver/samba.md
  - Helpers:
    - Pattern: pattern-fr.md
    - Cheat Sheet: cheat_sheet.md
    - Other Tests: test.md
```