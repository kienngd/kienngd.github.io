# How to use pnpm: a simple guide


## What is pnpm?

**pnpm** is a package manager for JavaScript.
It is like **npm** or **yarn**, but it is **faster** and uses **less disk space**.

Why?

* pnpm saves only **one copy** of each version of a package.
* Many projects can share the same files.
* This makes your computer cleaner and faster.

<!--more-->
---

## Basic Use Cases

### Install pnpm globally

Install pnpm on your system:

```bash
npm install -g pnpm
```

Now you can use `pnpm` in any project.

---

### Install packages for a project

Go to your project folder and run:

```bash
pnpm install
```

This will install all packages from `package.json`.

---

### Install one package

Add a package to your project:

```bash
pnpm add lodash
```

For development only:

```bash
pnpm add -D typescript
```

---

### Install a package globally

Use a tool everywhere:

```bash
pnpm add -g serve
```

---

## Other Common Commands

### Remove a package

Delete a package from your project:

```bash
pnpm remove lodash
```

---

### Update packages

Update all packages:

```bash
pnpm update
```

Update a specific package:

```bash
pnpm update lodash
```

---

### Install and run tests

Install dependencies and run tests:

```bash
pnpm install-test
```

This is useful to check if everything works after install.

---

### For help
```bash
pnpm --help
```

---

## Conclusion

pnpm is a smart, fast, and space-saving package manager.
With simple commands like **install**, **add**, **remove**, **update**, and **install-test**,
you can manage your project dependencies easily.

