# Machine Setup
## Typst
Working as of Typst 0.13.0.

## Tinymist
Version: 0.13.10

Configuration:

<details><summary>Neovim</summary>

```lua
vim.lsp.config.tinymist = {
  cmd = { 'tinymist' },
  filetypes = { 'typst' },
  root_markers = { 'main.typ', '.git' },
  settings = {
    -- Use your favourite pdf viewer that auto refreshes, e.g. sioyek
    exportPdf = "onSave",
    projectResolution = "lockDatabase",
    formatterMode = "typstyle",
  },
}
vim.lsp.enable("tinymist")
```
</details>

## Fonts 
### Open Sans
The template prefers Open Sans.
Typst does not support variable fonts as of 0.13.0.
Install the font files in `/dist/Open Sans/static/` following the `README.md` instructions.

### Font Awesome
Install `.otf` font files located in `/dist/fa-x.x.x-otf/`.
- Mac: Double click `.otf` file to install into Font Book.
- Windows: Right-click -> Install.
See Font Awesome [docs](https://docs.fontawesome.com/desktop/setup/get-started) for details specific to your OS.

# Folder structure
`eza -D -T -L 2`
```
├── main.typ            # Entry point of the resume
├── body                # Folder containing individual sections of your resume
│   └── <section>.typ   # The content of a resume section to be included
├── components          # Reusable components in your resume
├── data                # Data to be used in resume, e.g. profile photo
├── dist                # Distributed assets, e.g. fonts
└── template            # Contains the top-level template
```

## Resume structure
The resume consists of 5 top-level parts: `header`, `preamble`, `core`, `side`, and `postamble`, laid out as follows.
```
|----------------|
|     header     |
|----------------|
|    preamble    |
|----------------|
|          |     |
|   core   |side |
|          |     |
|----------------|
|    postamble   |
|----------------|
```

### Header
The header contains personal information, e.g. name, social media links, contact details.
It also contains a profile picture in the top-right corner.
This section is automatically generated based on the `author` dictionary in `main.typ`.

### Preamble
The preamble section is suitable for a top-level summary or personal statement.

### Core
The core takes up most of the area of the resume, and should likely contain details like work experience.

### Side
The side is a narrow version column adjacent to `core`, which may be convenient for short-form content like education, list of skills, languages etc.

### Postamble
The postamble is suitable for content that don't visually fit well in `core` or `side` to avoid too many line breaks, e.g. list of publications.


## Organisation recommendation
The intention of the project is for the resume to be composable, i.e. sections can be swapped in/out with little effect on layout.
This is especially useful if you want to have different versions of personal statements or work experience blocks, each of which might be phrased for a particular type of job application.

`main.typ` behaves like "config as code", where you can choose which input files are read during compilation and how they're arranged based on the overall structure of the resume.

# TODO
- Components: some way to configure styling across components, e.g. links are underlined blue? Read from a yaml config?

# FAQ
## Why isn't my font being used?
Assuming the font is correctly installed on your system, you may need to restart `tinymist` or `typst watch` so they can correctly reload the fonts.
If `tinymist` is running through your IDE as an LSP, you may need to restart your IDE.
