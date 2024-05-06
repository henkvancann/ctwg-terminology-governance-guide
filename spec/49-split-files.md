# How to split `terms_and_definitions.md` file into multiple files

## General info

Note:

- The JSON file `specs.unsplit.json` is a one time back-up of `specs.json`.
- When running the script below (`npm run split`) the JSON file `specs.unsplit.json` will be copied to `specs.json`. **Use this file to change the config since this is the source**.
- Make sure that at the end this entry **"account":"trustoverip"** is correctly set.
- The `spec.json file will have multiple new entries, one entry per defined term. The file can grow large.
- The file is written without newlines. If you want to make it readable, run a code beautifier.

## How to split terms_and_definitions.md

Split `terms_and_definitions.md` into multiple files, one file per term:

```
npm run split
```

Create the glossary file (named `index.html`):

```
npm run render
```
