# Local Development Guide

Quick reference for working on this site locally.

---

## Opening the site in your browser

Every time you want to preview or edit the site, you need to start the local dev server.

### Step 1 — Open PowerShell 7

Press `Win + S`, type **PowerShell 7**, and open it.

### Step 2 — Navigate to the project

```
cd C:\Users\lmalv\my-website
```

### Step 3 — Start the dev server

```
npm run dev
```

You'll see output like this:

```
astro v6.x.x ready in ...ms
  Local    http://localhost:4321/my-website
```

### Step 4 — Open the site

Go to your browser and visit:

```
http://localhost:4321/my-website
```

The site will **automatically update** in the browser whenever you save a file — no need to restart.

### Step 5 — Stop the server when done

Press `Ctrl + C` in the terminal.

---

## Opening Claude Code

Claude Code lets you edit the site with AI assistance directly from the terminal.

### Step 1 — Open PowerShell 7 and navigate to the project

```
cd C:\Users\lmalv\my-website
```

### Step 2 — Start Claude Code

```
claude
```

You can now describe changes you want to make and Claude will edit the files for you.

> Tip: You can run Claude Code and the dev server at the same time — just open two separate PowerShell 7 windows, one for each.

---

## Project folder location

```
C:\Users\lmalv\my-website
```

---

## Quick reference

| What                  | Command                          |
|-----------------------|----------------------------------|
| Start dev server      | `npm run dev`                    |
| Open site in browser  | http://localhost:4321/my-website |
| Open Claude Code      | `claude`                         |
| Stop dev server       | `Ctrl + C`                       |
| Build for production  | `npm run build`                  |
