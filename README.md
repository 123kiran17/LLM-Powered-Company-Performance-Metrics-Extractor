# LLM-Powered Company Performance Metrics Extractor

This project is an LLM-powered application that processes user queries related to company performance metrics and converts them into a structured JSON format. The application uses a combination of custom Named Entity Recognition (NER) models and the Gemini API to extract entities (company names), parameters (performance metrics), and date ranges from the queries.

## Features

- **Company & Parameter Detection**: Utilizes custom NER models to detect company names and performance metrics in user queries.
- **Date Range Handling**: Automatically assigns default date ranges (last one year) if not explicitly mentioned in the query.
- **LLM Integration**: Employs the Gemini API for generating structured JSON outputs from user queries.
- **History Handling**: Maintains context by tracking the last 4 queries to support follow-up questions.
- **Error Handling**: Includes robust error handling for JSON parsing and missing information.

## Setup Instructions

### Prerequisites

- Python 3.7+
- Install necessary Python packages:
  ```bash
  pip install spacy pandas python-gemini-api
  ```
- Gemini API cookies (required for accessing the Gemini API).

## File Structure

- **`companies.csv`**: Contains the list of company names.
- **`parameters.csv`**: Contains the list of performance metrics.
- **`company_ner_model`**: Pre-trained spaCy model for detecting company names.
- **`parameter_ner_model`**: Pre-trained spaCy model for detecting performance metrics.
- **`extract_entities.py`**: Python script containing the main logic for processing user queries.

## Usage

1. **Load the Data**:
    ```python
    companies_df = pd.read_csv("/content/companies.csv")
    parameters_df = pd.read_csv("/content/parameters.csv")
    ```

2. **Load the Models**:
    ```python
    nlp_model_1 = spacy.load("/content/company_ner_model")
    nlp_model_2 = spacy.load("/content/parameter_ner_model")
    ```

3. **Set Up the Gemini API Client**:
    ```python
    cookies = 'ENTER YOUR COOKIES'
    client = Gemini(cookies=cookies)
    ```

4. **Process Queries**:
    ```python
    queries = [
        "Get me Tesla revenue for the last one year",
        "Amazon profit for last one year"
    ]
    
    output = handle_queries(queries)
    print(output)
    ```
## Error Handling

- **Invalid JSON Response**: The application will handle JSON decoding errors and return a message indicating the issue, ensuring robustness when processing API responses.
  
- **Missing Information**: If any entity or parameter is missing from a user query, the application will attempt to fill in the gaps using information from previous queries or by applying default values.

## Future Enhancements

- **Support for Additional Date Formats**: Implement parsing for relative date ranges such as "last quarter" or "previous month" to provide more flexibility in user queries.

- **Enhanced NER Models**: Continuously improve the custom Named Entity Recognition (NER) models to increase accuracy in detecting entities (e.g., company names) and parameters (e.g., performance metrics).

## Dependencies

- **spaCy**: For natural language processing and entity recognition.
- **pandas**: For handling and processing data from CSV files.
- **python-gemini-api**: For interacting with the Gemini API to process user queries.

## Contributing
Contributions are welcome! Please fork the repository and submit a pull request with your changes.

For more details, please refer to the documentation and the project repository.
