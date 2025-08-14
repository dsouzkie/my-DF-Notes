# Assignment 1 — ExifTool Metadata Analysis

**Analyst:** Christy Dsouza  
**Date:** 2025-08-13
**Evidence:** `Forensics-image.png`

---

## 🔎 Image Overview
- **Filename:** Forensics-image.png
- **File Size:**  1144 kB
- **Image Dimensions:** 1439X753
- **File Signature (Magic Bytes):** `FF D8 FF E0 …` → **JPEG (JFIF + EXIF)** 89 50 4E 47 0D 0A 1A 0A

  - **Note:** Filename says `.png` but header is **JPEG** → renamed at some point.

## 📸 Camera / Software
- **Make:** Not Present
- **Model:** Not Present
- **Editing Software:** GIMP 2.10.24

## 🌍 Geolocation (if present)
- **GPS Latitude** No GPS data
- **Map Link:** None

## 🕐 Timestamps
- **DateTimeOriginal:** Not present
- **ModifyDate:** 2021:04:21 11:06:39
- **Comment on consistency:** none

## 🧰 Method (commands run)
```bash
# full dump
exiftool -a -u -g1 Forensics-image.png

# focused fields
exiftool -DateTimeOriginal -ModifyDate -Software -Make -Model -GPSLatitude -GPSLongitude -GPSAltitude Forensics-image.png

# xmp / icc
exiftool -X Forensics-image.png

# hex header (PowerShell)
Get-Content .\Forensics-image.png -Encoding Byte -TotalCount 32 | Format-Hex

# strings (PowerShell)
$bytes = [IO.File]::ReadAllBytes('.\Forensics-image.png')
$text  = -join ([char[]]$bytes)
[regex]::Matches($text,'[\x20-\x7E]{6,}') | % { $_.Value } | Select -First 40


## SHA 256 HASH 
:EFECB358E1ADE19D08ACF1126B846971982FB8B3A82F67BDF7401A8972FD241A   

## 🧠 Inference
The file header identifies the image as JPEG (JFIF + EXIF) despite a `.png` extension, indicating it was likely renamed. 
Camera EXIF fields (Make/Model) and GPS coordinates are absent, while the Software tag shows "GIMP 2.10.24", confirming the image was edited or exported using GIMP. 
Timestamps are missing, suggesting original metadata was stripped during editing. 
The image is not the untouched original but an edited/exported version.

