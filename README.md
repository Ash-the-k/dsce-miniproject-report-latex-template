# VTU Mini-Project Report — LaTeX Template

A clean, reusable LaTeX template for the **Dayananda Sagar College of Engineering**
VTU Mini-Project Report (Third Year, BE — CSE Data Science).

Built and maintained by students of the 2023–24 batch, Dept. of CSE (Data Science).

> **New to LaTeX?** Everything you need is in the [How to Use](#how-to-use) section below.
> The template also contains a full cheat sheet as the last chapter inside `main.tex`.

---

## Folder Structure

```
project-report-template/
├── main.tex                   ← Entire report source — only file you edit
├── references.bib             ← BibTeX references
├── README.md                  ← This file
├── images/
│   ├── VTULogo.png            ← Do not rename
│   ├── DSCELogo.png           ← Do not rename
│   ├── placeholder.png        ← Used by all figures until you replace them
│   ├── Diagrams/              ← Architecture diagrams, DFDs, use case diagrams
│   └── screenshots/           ← Dashboard and demo screenshots
└── appendix/                  ← Plagiarism report and AI detection PDFs
```

---

## How to Use

### Step 1 — Fill in your details

Open `main.tex` and find the block at the top marked **FILL THIS**. Update every command in that block:

| Command | What to put |
|---|---|
| `\ProjectTitle` | Full project title (can span two lines with `\\`) |
| `\HeaderTitle` | Short version for the page header (under 8 words) |
| `\AcademicYear` | e.g. `2025--2026` (two dashes = en-dash) |
| `\StudentOne` to `\StudentFour` | Full names of all team members |
| `\USNOne` to `\USNFour` | Corresponding USNs |
| `\GuideName` | Guide's full name |
| `\GuideDesignation` | Guide's designation and department |
| `\ProjectCoordinator` | Project coordinator's full name |
| `\HODName` | Head of Department's full name |
| `\PrincipalName` | Principal's full name |

---

### Step 2 — Compile

Run these four commands in your terminal from inside the project folder:

```bash
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

You need **four steps, not one**. The first `pdflatex` builds the document. `bibtex` processes references. The second and third `pdflatex` runs resolve cross-references and update the table of contents. If you only run once, figure numbers and citations will show as **[?]**.

**Using an editor instead:**

| Editor | Notes |
|---|---|
| **Overleaf** | Upload the full folder. Handles everything automatically. Recommended if you have no local LaTeX install. |
| **TeXstudio** | Click Tools → Build & View. Handles multi-pass automatically. |
| **VS Code** | Install the [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) extension. Compiles on save. |

---

### Step 3 — Add your images

All figures in the template use `images/placeholder.png` so compilation works out of the box. Create this file first:

```bash
cp images/VTULogo.png images/placeholder.png
```

Once your actual diagrams and screenshots are ready, replace the path inside each `\includegraphics` with your real file. Example:

```latex
% Before (placeholder)
\includegraphics[width=0.65\textwidth]{images/placeholder.png}

% After (your real file)
\includegraphics[width=0.65\textwidth]{images/Diagrams/high_level_arch.png}
```

**Image size options** — change the `width` value:

| Value | Result |
|---|---|
| `width=\textwidth` | Full page width |
| `width=0.9\textwidth` | 90% of page width |
| `width=0.65\textwidth` | 65% — good for portrait diagrams |
| `width=0.5\textwidth` | Half width |
| `width=5cm` | Fixed size |

**File naming tip:** Use lowercase names with underscores (`high_level_arch.png`). Avoid spaces and capital letters — they cause issues across operating systems.

---

### Step 4 — Add your references

Open `references.bib`. Each reference is one BibTeX block. Copy the sample that matches your source type and fill in the fields.

**Journal article:**
```bibtex
@article{smith2024stress,
  author  = {Smith, John and Doe, Jane},
  title   = {Title of the Paper},
  journal = {Name of Journal},
  volume  = {12},
  number  = {3},
  pages   = {100--115},
  year    = {2024},
  doi     = {10.xxxx/xxxxxx}
}
```

**Conference paper:**
```bibtex
@inproceedings{kumar2023eeg,
  author    = {Kumar, Raj and Singh, Priya},
  title     = {Title of the Paper},
  booktitle = {Proceedings of the Conference Name},
  pages     = {45--52},
  year      = {2023},
  doi       = {10.1109/xxxxxx}
}
```

**Website or dataset:**
```bibtex
@misc{dataset2022,
  author       = {Author, Name},
  title        = {Name of the Dataset or Website},
  year         = {2022},
  howpublished = {\url{https://example.com}},
  note         = {Accessed: January 2024}
}
```

The key (e.g. `smith2024stress`) is what you use to cite in text:

```latex
According to Smith et al.~\cite{smith2024stress}, ...
```

Use `~` (tilde) before `\cite` — it adds a non-breaking space so the number never wraps onto a new line alone.

---

### Step 5 — Add appendix PDFs

Place your PDFs in the `appendix/` folder, then update the filenames in the `\includepdf` calls at the bottom of `main.tex`. The template already has two slots (plagiarism report and AI detection report).

To add more PDFs, copy this block and paste it inside the Appendix chapter:

```latex
\section{Your Section Title}

Brief description of this document.

\includepdf[
    pages=-,
    pagecommand={\thispagestyle{mainstyle}}
]{appendix/your_file.pdf}
```

`pages=-` means all pages. For specific pages: `pages={1,3,5}` or a range: `pages={2-4}`.

---

## Quick Reference

### Text formatting

```latex
\textbf{bold text}         % Bold
\textit{italic text}       % Italic
\texttt{code or filename}  % Monospace / inline code
```

### Lists

```latex
% Bullet list
\begin{itemize}
    \item First point
    \item Second point
\end{itemize}

% Numbered list
\begin{enumerate}
    \item First step
    \item Second step
\end{enumerate}
```

### Headings

```latex
\section{Section Title}
\subsection{Subsection Title}
```

### Inserting an image

```latex
\begin{figure}[H]
    \centering
    \includegraphics[width=0.75\textwidth]{images/Diagrams/your_image.png}
    \caption{Your caption text here}
    \label{fig:your_label}
\end{figure}
```

Refer to it in text with:
```latex
The diagram is shown in Figure~\ref{fig:your_label}.
```

### Code block

```latex
\begin{lstlisting}[language=Python, caption={Your caption}, label={code:your_label}]
# your code here
print("Hello")
\end{lstlisting}
```

Supported languages: `Python`, `bash`, `TeX`, `SQL`, `Java`, `C`, `C++`

### Special characters

| Character | LaTeX command |
|---|---|
| `%` | `\%` (plain `%` starts a comment) |
| `&` | `\&` |
| `_` | `\_` |
| `\` | `\textbackslash` |
| `~` | `\textasciitilde` |
| en-dash (–) | `--` |
| em-dash (—) | `---` |

---

## Common Issues

| Problem | Fix |
|---|---|
| `[?]` instead of figure/citation numbers | Run the full 4-step compile sequence |
| `File not found` for an image | Check the path and filename — it is case-sensitive |
| PDF not attaching in appendix | Confirm the PDF is in `appendix/` and the filename in `\includepdf` matches exactly |
| Table of contents not updating | Run the full 4-step compile sequence |
| Compilation fails completely | Check the line number in the error message — it points to the exact problem |

---

## Credits

Created by [Ashlesh Kanchan](https://github.com/Ash-the-k/) — Dept. of CSE (Data Science), DSCE, Batch 2023–24.

Originally built for our own project, then cleaned up and generalized as a reusable template for future batches.

---

## License

MIT License — free to use, modify, and share with attribution. See [`LICENSE`](LICENSE) for details.