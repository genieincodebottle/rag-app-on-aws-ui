# RAG Application on AWS

A Streamlit-based web application for Retrieval-Augmented Generation (RAG) using Amazon Web Services.

## Related Projects

- [RAG Backend](https://github.com/genieincodebottle/rag-app-on-aws): The AWS Infra provisioing and related RAG backend codes.

## Application Flow diagrams

- [Authentication Flow](https://github.com/genieincodebottle/rag-app-on-aws-ui/blob/main/images/auth_sequence.png)
- [Doc Upload Flow](https://github.com/genieincodebottle/rag-app-on-aws-ui/blob/main/images/document_upload_sequence.png)
- [Doc Processing Flow](https://github.com/genieincodebottle/rag-app-on-aws-ui/blob/main/images/doc_processing_sequence.png)
- [Query Processing Flow](https://github.com/genieincodebottle/rag-app-on-aws-ui/blob/main/images/query_processing_sequence.png)

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [System Architecture](#system-architecture)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Endpoints](#api-endpoints)
- [Authentication](#authentication)
- [Document Management](#document-management)
- [Contributing](#contributing)
- [License](#license)

## Overview

This RAG (Retrieval-Augmented Generation) application provides a web-based interface for uploading documents, querying them using natural language, and retrieving AI-generated responses based on the document content. The application uses AWS services for authentication, document storage, indexing, and AI processing.

## Features

- **User Authentication**:
  - Registration, login, and password reset functionality
  - Token-based authentication with auto-refresh
  - Email verification

- **Document Management**:
  - Upload various document types (PDF, DOCX, TXT, CSV, etc.)
  - View uploaded documents
  - Associate documents with user IDs

- **Querying Capabilities**:
  - Natural language queries against uploaded documents
  - AI-generated responses based on document content
  - Relevance scoring for retrieved documents
  - Query history tracking

- **User Interface**:
  - Clean, responsive Streamlit interface
  - Tabbed views for different application sections
  - Detailed error reporting and status updates

## System Architecture

The application follows a client-server architecture:

1. **Frontend**: Streamlit web application
2. **Backend**: AWS services including:
   - API Gateway for RESTful API endpoints
   - Lambda functions for processing
   - Cognito for user authentication
   - S3 for document storage
   - OpenSearch/vector database for document indexing and retrieval
   - AWS Bedrock or similar for AI generation

## Prerequisites

- Python 3.8+
- Streamlit 1.45.0+
- AWS Account with appropriate services configured
- API endpoints for authentication, document upload, and querying

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/rag-app-aws.git
   cd rag-app-aws
   ```

2. Create a virtual environment:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

## Configuration

1. Create a `.env` file in the project root with the following variables:
   ```
   API_BASE_URL=https://your-api-gateway-url.amazonaws.com/stage
   API_KEY=your_api_key_if_needed
   DEFAULT_USER_ID=test-user
   UPLOAD_ENDPOINT=/upload
   QUERY_ENDPOINT=/query
   AUTH_ENDPOINT=/auth
   COGNITO_CLIENT_ID=your_cognito_client_id
   ```

2. Configure your AWS services:
   - Set up Cognito User Pool for authentication
   - Configure API Gateway with appropriate endpoints
   - Set up Lambda functions for backend processing
   - Configure S3 buckets for document storage
   - Set up OpenSearch or vector database for document indexing

## Usage

1. Start the Streamlit application:
   ```
   streamlit run app.py
   ```

2. Access the application in your web browser at `http://localhost:8501`

3. Register a new account or log in with existing credentials

4. Upload documents, query them, and view AI-generated responses

## API Endpoints

The application interacts with the following API endpoints:

### Authentication Endpoint (`/auth`)

Handles various authentication operations:
- `register`: Register new user
- `verify`: Verify user email
- `login`: Authenticate user and get tokens
- `refresh_token`: Refresh authentication tokens
- `forgot_password`: Initiate password reset
- `confirm_forgot_password`: Complete password reset

### Upload Endpoint (`/upload`)

Handles document uploads:
- Accepts file content, metadata, and user ID
- Returns document ID and status

### Query Endpoint (`/query`)

Handles document queries:
- Accepts natural language query and user ID
- Returns AI-generated response and relevant document excerpts

## Authentication

The application uses Amazon Cognito for user authentication with JWT tokens:

1. **Registration Process**:
   - User registers with email, password, and optional name
   - Verification code sent to email
   - User verifies email with code

2. **Login Process**:
   - User logs in with email and password
   - Receives access token, ID token, and refresh token
   - Tokens automatically refresh before expiry

3. **Password Reset**:
   - User initiates forgot password
   - Confirmation code sent to email
   - User resets password with code and new password

## Document Management

Documents uploaded to the system are:

1. Converted to text using appropriate extractors
2. Chunked into smaller segments
3. Embedded into vector representations
4. Indexed for semantic search
5. Associated with the user ID for retrieval


**Note**: This RAG application is designed to work with AWS services.