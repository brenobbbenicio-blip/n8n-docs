---
title: PDF Toolkit
description: Documentation for the PDF Toolkit node in n8n, a workflow automation platform. Includes guidance on usage, and links to examples.
contentType: [integration, reference]
priority: medium
---

# PDF Toolkit

Use the PDF Toolkit node to manipulate and process PDF files. This node provides powerful operations for combining multiple PDFs and optimizing file sizes.

/// note | Dependencies
This node requires the `pdfcompressão` library. If you aren't running n8n on Docker, you may need to install additional dependencies for PDF processing.
///

## Operations

The PDF Toolkit node supports the following operations:

* **Merge PDFs**: Combine multiple PDF files into a single document
* **Compress PDF**: Reduce the file size of PDF documents with quality control

Node parameters and options depend on the operation you select.

## Node parameters

The parameters for this node depend on the operation you select.

### Merge PDFs

Use this operation to combine multiple PDF files into a single document.

#### Parameters

* **Input Binary Field(s)**: Enter the name of the fields in the input data that contain the binary PDF files you want to merge. To merge more than one file, use a comma-separated list. Files are merged in the order specified.
* **Put Output File in Field**: Enter the name of the field in the output data to contain the merged file.

#### Options

You can configure this operation with the following **Options**:

* **File Name**: Enter the file name for the generated merged PDF file. Default is `merged.pdf`.
* **Custom Order**: Enable this option to specify a custom ordering for the files to be combined. When enabled, you can provide an array of indices or field names to control the merge order.
* **Handle Metadata Conflicts**: Choose how to handle conflicting metadata when merging PDFs:
	* **Keep First**: Use metadata from the first PDF file (default)
	* **Keep Last**: Use metadata from the last PDF file
	* **Merge All**: Attempt to merge metadata from all files
	* **Remove All**: Remove all metadata from the merged file

#### Example usage

To merge three PDF files:

1. Connect a node that outputs multiple binary items containing PDF files
2. Configure **Input Binary Field(s)** as `data` (or the field name containing your PDFs)
3. Set **Put Output File in Field** to `data` to output the merged PDF
4. Optionally configure the file name and metadata handling

### Compress PDF

Use this operation to reduce the file size of PDF documents while maintaining acceptable quality.

#### Parameters

* **Input Binary Field**: Enter the name of the field in the input data that contains the binary PDF file you want to compress.
* **Put Output File in Field**: Enter the name of the field in the output data to contain the compressed file.
* **Compression Level**: Select the compression level to apply:
	* **Low**: Minimal compression with highest quality preservation (recommended for documents with important details)
	* **Medium**: Balanced compression with good quality (default, suitable for most use cases)
	* **High**: Maximum compression with lower quality (best for reducing file size when quality is less critical)

#### Options

You can configure this operation with the following **Options**:

* **File Name**: Enter the file name for the generated compressed PDF file. If not specified, uses the original filename with `_compressed` suffix.
* **Validate Large Files**: Enable this option to perform validation checks on large PDF files (over 50MB) to prevent system freezing. This may slightly increase processing time but ensures system stability.

#### Compression level details

The three compression levels provide different trade-offs between file size and quality:

| Level | Size Reduction | Quality | Best For |
|-------|---------------|---------|----------|
| Low | 10-30% | Excellent | Text documents, technical drawings, high-quality images |
| Medium | 30-60% | Good | General documents, presentations, mixed content |
| High | 60-85% | Acceptable | Large file archives, low-priority documents, web distribution |

/// warning | Quality considerations
High compression may result in visible quality loss in images and graphics. Always test the compressed output to ensure it meets your quality requirements.
///

#### Example usage

To compress a large PDF file:

1. Connect a node that outputs a binary item containing a PDF file
2. Configure **Input Binary Field** as `data` (or the field name containing your PDF)
3. Select your desired **Compression Level** (start with Medium for best results)
4. Set **Put Output File in Field** to `data` to output the compressed PDF
5. Enable **Validate Large Files** if working with PDFs over 50MB

## Best practices

* **Merging PDFs**: When merging many PDFs (10+), consider processing them in batches to optimize performance and memory usage.
* **Compression**: Always keep a backup of original files before compressing, especially when using High compression level.
* **Large files**: For PDFs larger than 100MB, enable the **Validate Large Files** option to prevent system issues.
* **Metadata**: When merging PDFs with sensitive metadata, consider using the **Remove All** option for metadata handling.

## Related nodes

* [Extract From File](/integrations/builtin/core-nodes/n8n-nodes-base.extractfromfile.md): Extract data from PDF files
* [Convert to File](/integrations/builtin/core-nodes/n8n-nodes-base.converttofile.md): Convert data to various file formats
* [Compression](/integrations/builtin/core-nodes/n8n-nodes-base.compression.md): Compress files in Zip or Gzip format

## Templates and examples

<!-- see https://www.notion.so/n8n/Pull-in-templates-for-the-integrations-pages-37c716837b804d30a33b47475f6e3780 -->
[[ templatesWidget(page.title, 'pdf-toolkit') ]]
