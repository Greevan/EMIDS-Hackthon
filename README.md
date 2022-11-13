# EMIDS-Hackthon(CODE USED FROM invoice2data (open-source)python library)
Hackthon organised by IIIT on Nov 11-13 2022
#Installation
Install pdftotext
If possible get the latest xpdf/poppler-utils version. It's included with macOS Homebrew, Debian and Ubuntu. Without it, pdftotext won't parse tables in PDF correctly.

Install invoice2data using pip

pip install invoice2data

Installation of input modules
An tesseract wrapper is included in auto language mode. It will test your input files against the languages installed on your system. To use it tesseract and imagemagick needs to be installed. tesseract supports multiple OCR engine modes. By default the available engine installed on the system will be used.

Languages: tesseract-ocr recognize more than 100 languages For Linux users, you can often find packages that provide language packs:

# Display a list of all Tesseract language packs
apt-cache search tesseract-ocr

# Debian/Ubuntu users
apt-get install tesseract-ocr-chi-sim  # Example: Install Chinese Simplified language pack

# Arch Linux users
pacman -S tesseract-data-eng tesseract-data-deu # Example: Install the English and German language packs

Usage
Basic usage. Process PDF files and write result to CSV.

invoice2data invoice.pdf
invoice2data invoice.txt
invoice2data *.pdf
Choose any of the following input readers:

pdftotext invoice2data --input-reader pdftotext invoice.pdf
pdftotext invoice2data --input-reader text invoice.txt
tesseract invoice2data --input-reader tesseract invoice.pdf
pdfminer.six invoice2data --input-reader pdfminer invoice.pdf
pdfplumber invoice2data --input-reader pdfplumber invoice.pdf
gvision invoice2data --input-reader gvision invoice.pdf (needs GOOGLE_APPLICATION_CREDENTIALS env var)
Choose any of the following output formats:

csv invoice2data --output-format csv invoice.pdf
json invoice2data --output-format json invoice.pdf
xml invoice2data --output-format xml invoice.pdf
Save output file with custom name or a specific folder

invoice2data --output-format csv --output-name myinvoices/invoices.csv invoice.pdf

Note: You must specify the output-format in order to create output-name

Specify folder with yml templates. (e.g. your suppliers)

invoice2data --template-folder ACME-templates invoice.pdf

Only use your own templates and exclude built-ins

invoice2data --exclude-built-in-templates --template-folder ACME-templates invoice.pdf

Processes a folder of invoices and copies renamed invoices to new folder.

invoice2data --copy new_folder folder_with_invoices/*.pdf

Processes a single file and dumps whole file for debugging (useful when adding new templates in templates.py)

invoice2data --debug my_invoice.pdf

Recognize test invoices: invoice2data invoice2data/test/pdfs/* --debug
