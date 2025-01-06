
# XML Invoice Processor

The **XML Invoice Processor** is a Python-based tool designed to process XML invoices, convert them into PDF format, and save them in a timestamped directory. The tool supports processing embedded XSLT stylesheets within the XML files and provides a fallback mechanism to use a default XSLT stylesheet when embedded XSLTs are not available or invalid.

## Features

- **Batch Processing:** Automatically processes all XML files in the specified input directory.
- **Embedded XSLT Support:** Extracts and applies embedded XSLT stylesheets for transformation.
- **Fallback Mechanism:** Utilizes a default XSLT stylesheet when no embedded XSLT is available or valid.
- **PDF Conversion:** Converts the transformed XML data into PDF format using the `pdfkit` library.
- **Error Handling:** Captures and reports errors during XML processing, XSLT transformation, and PDF generation.
- **Timestamped Output Directory:** Organizes generated PDFs in directories named by the current date.

## Requirements

- Python 3.6+
- Libraries:
  - `os`
  - `base64`
  - `tempfile`
  - `pdfkit`
  - `lxml`
- `wkhtmltopdf` executable installed and its path configured.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/QuarksG/e-invoice-XML-converter-to-PDF.git
   cd https://github.com/QuarksG/e-invoice-XML-converter-to-PDF.git
   ```
2. Install the required Python libraries:
   ```bash
   pip install pdfkit lxml
   ```
3. Install `wkhtmltopdf` and ensure it is accessible in your system PATH.
   ```bash
   sudo apt-get install wkhtmltopdf
   ```
   Or download it from [wkhtmltopdf](https://wkhtmltopdf.org/).

## Usage

### Initialize the Processor

Create an instance of `XMLInvoiceProcessor` by providing:

- The directory containing XML invoices.
- The output directory for saving PDFs.
- The path to the `wkhtmltopdf` executable.
- The path to the default XSLT file.

Example:

```python
from XMLInvoiceProcessor import XMLInvoiceProcessor

xml_dir = "/path/to/xml/files"
output_dir = "/path/to/output/files"
wkhtmltopdf_path = "/usr/local/bin/wkhtmltopdf"
default_xslt_path = "/path/to/default/stylesheet.xslt"

processor = XMLInvoiceProcessor(xml_dir, output_dir, wkhtmltopdf_path, default_xslt_path)
```

### Process Invoices

Invoke the `xml_to_pdf_and_tally` method to start processing XML invoices:

```python
processor.xml_to_pdf_and_tally()
```

### File Structure

- **Input Directory:** Contains XML files to be processed.
- **Output Directory:** Contains timestamped folders with generated PDF files.

## Error Handling

- If an embedded XSLT is invalid or missing, the processor falls back to the default XSLT.
- Errors encountered during processing are printed to the console with details for debugging.

## Example XML File

```xml
<Invoice xmlns="urn:oasis:names:specification:ubl:schema:xsd:Invoice-2"
         xmlns:cbc="urn:oasis:names:specification:ubl:schema:xsd:CommonBasicComponents-2"
         xmlns:cac="urn:oasis:names:specification:ubl:schema:xsd:CommonAggregateComponents-2">
  <cbc:ID>INV-12345</cbc:ID>
  <cac:Attachment>
    <cbc:EmbeddedDocumentBinaryObject mimeCode="application/xml">Base64EncodedXSLT</cbc:EmbeddedDocumentBinaryObject>
  </cac:Attachment>
</Invoice>
```

## Development Notes

- Ensure the default XSLT file is correctly formatted and tested for compatibility.
- Update the namespaces in the code if using a different UBL (Universal Business Language) schema version.

## Troubleshooting

1. **PDF Not Generated:**
   - Check the `wkhtmltopdf` path configuration.
   - Ensure the input XML file contains valid data.
2. **Invalid XSLT Error:**
   - Verify that the embedded or default XSLT is valid and conforms to XML syntax.
3. **Missing Invoice Numbers:**
   - Ensure the `<cbc:ID>` tag exists in the XML file.

## License

This project is licensed under the MIT License.

## Contribution

Contributions are welcome! Feel free to fork the repository and submit pull requests for improvements or new features.



