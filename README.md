# Tailwind CSS Bug Report

@author [Lusayo](https://github.com/lusayo-nyondo)

## TLDR
- `npx tailwindcss -i ./src/input.css -o ./src/output.css --watch` fails to watch the file system and trigger hot reloads if any of the parent directories containing the project have parenthesis in their name.

## Context
I encountered this issue while I was setting up tailwind for use within my Django Project. I store my git repos inside the path: `D:/Programs (SSD)/GitHub/`.

The project in which I was trying to install tailwind was located at `D:/Programs (SSD)/GitHub/sayo_portfolio`.

Omitting a lot of details, my project essentially had the following file structure:

```bash
...
├── src
│   └── input.css
└── static
    └── src
        └── input.css
        └── output.css
└── templates
    └── index.html
    ...
```

My tailwind config file contained the config:
```bash
module.exports = {
    content: [
        './templates/**/*.html',
    ],
    theme: {
        extend: {},
    },
    plugins: [],
    }
```

From within the project directory, running `npx tailwindcss -i ./src/input.css -o ./src/output.css --watch` did not trigger the hot reloads and update the `output.css` file when I updated the contents of `templates/index.html`.

I have recreated a demonstration of the bug in this repo.

## Reproducing the bug
- Clone this repository
- Navigate to `tailwind_(lab)`
- Run `npm install`
- Run `npx tailwindcss -i ./src/input.css -o ./src/output.css --watch`
- Open the `templates/index.html` file in your browser to view how it renders. It's just a centered div with `bg-slate-700`.
- Modify the background color of the div to `bg-blue-700` and save.
- Refresh the browser to see the change.
- Done.

For me, following the steps above, it doesn't work.

## Solution
Renaming the parent folder of the project to not have parenthesis.

## My Environment:

node v20.12.2

tailwindcss v3.4.13

windows 11:
        Major  Minor  Build  Revision
        -----  -----  -----  --------
        10     0      21996  0