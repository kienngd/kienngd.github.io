# Manage Your PDF Files Easily with pdfcpu


# Manage Your PDF Files Easily with pdfcpu

If you are looking for a powerful tool to handle PDF files, **pdfcpu** is the best choice. It is a fast, open-source PDF processor written in Go. You can use it as a command-line tool or as a library in your Go projects.

---

## Key Features
* **Extract/Trim:** Select and save specific pages.
* **Merge:** Join multiple PDF files into one.
* **Split:** Divide a large PDF into smaller files.
* **Optimize:** Reduce PDF file size.
* **Security:** Add or remove passwords and watermarks.
<!--more-->
---

## How to Download from GitHub
You can download the pre-built binaries for your operating system (Windows, Linux, or macOS) from the official GitHub page:

1.  Go to [github.com/pdfcpu/pdfcpu/releases](https://github.com/pdfcpu/pdfcpu/releases).
2.  Find the latest version (e.g., `v0.11.1`).
3.  Download the `.tar.xz` or `.zip` file for your system (e.g., `Linux_x86_64`).
4.  Extract the file and move the `pdfcpu` binary to your `/usr/local/bin` folder.

---

## Common Use-Cases

Here are some simple commands to get you started:

### 1. Extract pages (Save each page as a new file)
If you want to pull out pages 1 to 3 and save them as separate files:
```bash
pdfcpu extract -mode page -pages 1-3 input.pdf .
```

### 2. Trim pages (Create a new file with only specific pages)
If you want to create a new file named `output.pdf` containing only pages 1, 2, and 3:
```bash
pdfcpu trim -pages 1-3 input.pdf output.pdf
```

### 3. Merge files
To combine `part1.pdf` and `part2.pdf` into a single file:
```bash
pdfcpu merge merged.pdf part1.pdf part2.pdf
```

### 4. Optimize a file
To make your PDF file smaller for emailing:
```bash
pdfcpu optimize input.pdf
```

---

## Conclusion
**pdfcpu** is small but very powerful. It is perfect for developers and users who love simple command-line tools. Give it a try and save your time today!

