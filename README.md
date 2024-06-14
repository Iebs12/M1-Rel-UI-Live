# M1-Relevancy

This project is a Flask-based web application designed to predict the relevancy of documents to a given query. It processes Excel files containing document data, analyzes the content using advanced NLP techniques, and updates the file with relevancy predictions and comments.

## Table of Contents

1. [Overview](#overview)
2. [Features](#features)
3. [Setup and Installation](#setup-and-installation)
4. [Project Structure](#project-structure)
5. [How It Works](#how-it-works)
    - [Main Components](#main-components)
    - [Detailed Explanation](#detailed-explanation)
6. [Usage](#usage)
7. [Dependencies](#dependencies)
8. [API Endpoints](#api-endpoints)
9. [Contributing](#contributing)
10. [License](#license)

## Overview

This application leverages Flask for the web server, OpenAI for natural language processing, and Openpyxl for Excel file handling. It reads document data from an Excel file, processes each document to determine its relevancy to a specified query, and updates the file with the relevancy status and comments.

## Features

- Extracts document data from Excel files.
- Uses OpenAI's language model for relevancy prediction.
- Supports custom queries for relevancy assessment.
- Updates the original Excel file with prediction results and comments.
- Provides an easy-to-use web interface for file processing.

## Setup and Installation

### Prerequisites

- Python 3.7 or higher
- Pip (Python package installer)

### Installation Steps

1. **Clone the Repository**:
    ```bash
    git clone https://github.com/yourusername/flask-relevancy-prediction.git
    cd flask-relevancy-prediction
    ```

2. **Create a Virtual Environment**:
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```

3. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4. **Set Up Environment Variables**:
    Create a `.env` file in the root directory with the following content:
    ```bash
    LLAMA_CLOUD_API_KEY=your_openai_api_key
    ```

5. **Run the Application**:
    ```bash
    python app.py
    ```

6. **Access the Application**:
    Open your web browser and go to `http://localhost:5000`.

## Project Structure

```plaintext
.
├── app.py                # Main application file
├── requirements.txt      # Python dependencies
├── .env                  # Environment variables
└── README.md             # Project documentation
```
## How It Works

### Main Components

1. **Flask Application**:
    - Hosts the web interface and handles HTTP requests.
    - Defines routes for file processing.

2. **Excel Data Extraction**:
    - Uses `openpyxl` to read document data from Excel files.
    - Extracts specific columns for analysis.

3. **Relevancy Prediction**:
    - Leverages `llama_index` and OpenAI's language model for predicting document relevancy to a query.
    - Processes the content and generates relevancy status and comments.

4. **File Update**:
    - Adds relevancy results and comments to new columns in the original Excel file.
    - Saves the updated file.

### Detailed Explanation

1. **Flask Application Setup**:
    - The application is initialized using Flask.
    - The route `/` is defined to handle file upload and processing requests via POST method.

2. **Data Extraction**:
    - The `extractor` function reads an Excel file using `openpyxl`.
    - It retrieves data from specific columns and stores them in a list of dictionaries for further processing.

3. **Relevancy Prediction**:
    - The `backend` function processes each document using a custom Query Engine based on OpenAI's GPT-3.5.
    - The engine predicts whether the document is relevant to the given query.
    - It returns a tuple with a relevancy flag and a reason for the prediction.

4. **File Update**:
    - The `newFileSaver` function writes the relevancy results back to the Excel file.
    - It creates new columns for storing the relevancy status and comments.
    - The updated file is saved and its path is returned.

5. **API Endpoint**:
    - The `/` endpoint processes incoming JSON data containing the query and file path.
    - It calls the relevant functions to extract data, predict relevancy, and save results.
    - Returns the path to the updated file as a JSON response.

## Usage

1. **Upload and Process File**:
    - Send a POST request to the root endpoint with JSON data containing `query` and `file_path`.

    Example JSON:
    ```json
    {
        "query": "Is Mannuronic acid used in cosmetic formulations?",
        "file_path": "path/to/excel_file.xlsx"
    }
    ```

2. **View Results**:
    - Check the returned file path in the JSON response to view the updated Excel file.

## Dependencies

- **Flask**: Web framework for Python.
- **openpyxl**: Library for reading and writing Excel files.
- **dotenv**: Library for managing environment variables.
- **llama_index**: Custom library for indexing and querying document data.
- **OpenAI**: Python library for interacting with OpenAI's GPT-3.5.

## API Endpoints

- **`/`**: Main endpoint to process file and query.
    - **Method**: POST
    - **Request Body**:
        - `query`: The user query string.
        - `file_path`: Path to the Excel file.
    - **Response**:
        - `Path`: Updated file path.

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
