# Smart QC Code Extractor & Nomenclature Engine

An enterprise-grade desktop utility engineered to enforce strict document naming conventions (nomenclature) and automate the extraction of consultant approval codes directly from annotated PDF drawings using spatial analysis.

## ⚠️ Repository Note
*This repository serves as a portfolio showcase of the architectural logic, spatial PDF parsing techniques, and UI/UX design. The proprietary Python source code is withheld to protect intellectual property.*

## 🚧 The Problem
In the construction industry, submittals and Inspection Requests (IRs) are returned by consultants with manual stamps or **digital colored markups (varying wildly in color and style between different consultants)** indicating the approval status (Code A, B, C, or D). 
1. **Manual Data Entry:** Document Controllers must open hundreds of PDFs daily just to check the stamp and log the code into an Excel tracker.
2. **Naming Inconsistencies:** Files and ZIP archives are often named chaotically by different engineers, breaking the project's strict naming conventions and causing sorting collisions.

## 💡 The Solution & Core Features

### 1. Color-Agnostic Spatial PDF Analysis (Automated QC Extraction)
* **Universal Geometry Detection:** Utilizes `PyMuPDF` to scan PDF pages for specific geometric shapes (e.g., bounding boxes or rectangles) drawn by consultants to highlight approval codes, **regardless of the markup color used (Red, Blue, Green, etc.)**.
* **Coordinate-Based Text Extraction:** Once a markup boundary is detected, the engine calculates the coordinates and extracts the text (A, B, C, or D) located within or immediately adjacent to the bounding box.
* **Auto-Logging:** Generates a fully styled `openpyxl` Excel tracker detailing the file name, revision, and the spatially extracted QC Code (color-coded in the Excel sheet for quick visual sorting).

### 2. Intelligent Nomenclature Engine (Folder & Archive Renamer)
* **Regex-Driven Standardization:** Automatically parses messy folder and archive names (`.zip`, `.rar`, `.7z`), strips out arbitrary spaces around hyphens, and formats the text into strict Title Case.
* **Smart Preservation:** Intelligently preserves data within brackets `()` or `[]` while standardizing the surrounding string to prevent data loss.
* **Dry Run Mode & Collision Prevention:** Features a 'Dry Run' simulation mode and collision detection to prevent accidental overwriting of identically named targets on case-insensitive file systems (like Windows).

## 🛠 Tech Stack & Architecture
* **PDF Parsing & Spatial Analysis:** `PyMuPDF` (`fitz`) for advanced document geometry and text-block coordinate extraction.
* **GUI Framework:** `customtkinter` featuring a modern, multi-tabbed Dark Mode interface.
* **Data Export:** `openpyxl` for dynamic, formatted Excel generation with custom cell coloring and frozen panes.
* **Concurrency:** `threading` to keep the UI responsive during batch processing of massive directories.

## 📸 Interface Preview

![Folder Renamer Tab](main-dashboard.png.png)
