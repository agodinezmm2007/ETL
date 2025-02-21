# ETL data pre-processing for RAG

## Overview
This project implements an end-to-end ETL (Extract, Transform, Load) pipeline to be combined with a Retrieval Augmented Generation (RAG) system for processing research articles. 
The pipeline retrieves articles from PubMed and OpenAlex, downloads PDFs via Unpaywall, extracts text and tables using Azure Document Intelligence, integrates with Zotero for 
citation management, and uses an LLM (via OpenAI) to extract additional structured data from article content.

## Features
- **PubMed Search:** Retrieve article PMIDs and metadata.
- **OpenAlex Search:** Fetch articles and metadata using PyAlex.
- **PDF Retrieval:** Download PDFs via the Unpaywall API.
- **PDF Processing:** Extract text and tables from PDFs using Azure Document Intelligence.
- **Zotero Integration:** Upload PDFs to Zotero and generate formatted citations.
- **Additional Data Extraction:** Use OpenAI’s GPT-based model to extract fields such as study type, scenarios, and metrics.
- **Deduplication:** Merge and deduplicate articles based on DOI or Title.

- ## Installation
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/agodinezmm2007/ETL.git
   cd ETL
   pip install -r requirements.txt
2. Install Dependencies: Ensure you have Python 3.7+ installed, then run:
   
   ```pip install -r requirements.txt```
   
4. Install Jupyter: If you don't have it already, install Jupyter Notebook (or JupyterLab) by running:
   
     ```pip install notebook```
  
   or
   
     ```pip install jupyterlab```
  
5. Configure the Project:
   * Update the configuration section in the script with your API keys, email addresses, endpoints, and file paths.
   * Download the required CSL style files (e.g., from [Zotero Styles](https://www.zotero.org/styles)) and update the paths accordingly.
   
- ## Usage
  - Run the pipeline with:
    * Open the notebook file ETL_sanitized.ipynb in your preferred Jupyter environment (such as Jupyter Notebook, JupyterLab, or VS Code's Jupyter extension).
    * Run all cells in the notebook.
  - Follow the interactive prompts:
    * Enter your search queries (one per line).
    * Choose your citation style.
    * Select the data sources (PubMed, OpenAlex, or both).
    * Specify the maximum number of articles to retrieve per query.
    * The pipeline will process the data and save the final output as Feather files in the specified directory.

- ## Pipeline Steps
  * Collect Queries: Prompt the user for search queries.
  * Citation Style Selection: Choose the citation style for formatting.
  * Data Source Selection: Choose between PubMed, OpenAlex, or both.
  * Article Retrieval: Retrieve metadata from the chosen sources.
  * Deduplication: Merge results and remove duplicate entries.
  * PDF Retrieval: Download PDFs using the Unpaywall API.
  * Zotero Integration: Add PDFs to Zotero and generate citations.
  * Azure Extraction: Extract text and tables from PDFs via Azure Document Intelligence.
  * Field Extraction: Use an LLM (via OpenAI) to extract additional fields from the content.
  * Final Output: Save results to Feather files for further analysis.
 
- ## Code Structure
  * Configuration Section: API keys, email addresses, file paths, and Zotero settings.
  * Function Modules:
      * pubmed_search_chunked() – Retrieves PMIDs from PubMed.
      * fetch_pubmed_metadata() – Fetches metadata for retrieved PMIDs.
      * pyalex_search_works() – Searches and retrieves articles from OpenAlex.
      * get_pdf_from_unpaywall() – Downloads PDFs via Unpaywall.
      * AzurePDFExtractor – Class that wraps Azure Document Intelligence for text and table extraction.
      * deduplicate_by_doi_title() – Deduplicates articles based on DOI or title.
      * add_pdf_to_zotero() and get_citation_csl_json() – Handle Zotero integration and citation formatting.
      * extract_additional_fields() – Uses OpenAI’s GPT model to extract domain specific data.
      * pipeline() – Orchestrates the complete ETL process.
- ## Configuration
  Make sure to update:
    * API Keys/Endpoints: AZURE_KEY, AZURE_ENDPOINT, OPEN_API_KEY, ZOTERO_API_KEY, and emails.
    * Directories: Paths for logs, PDFs, output CSV/Feather files, etc.
    * Citation Styles: Paths to your downloaded CSL files.
- ## License
  This project is licensed under the [MIT License](https://github.com/agodinezmm2007/ETL/blob/main/LICENSE)

- ## Contributing
  Contributions are welcome! Feel free to fork the repository and submit pull requests.

- # Contact
  For any questions or issues, please contact agodinez@albany.edu
