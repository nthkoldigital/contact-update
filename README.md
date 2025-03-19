# Google Contacts Sync

A Google Colab notebook that syncs contact information between a CSV file and Google Contacts, using Organization Name as the unique identifier.

## Overview

This tool allows you to:
- Import contacts from a CSV file into Google Contacts
- Update existing contacts if they already exist (matched by Organization Name)
- Create new contacts if they don't exist
- Selectively update only fields that have changed
- Track all changes with detailed logs

## Prerequisites

1. A Google account with access to Google Contacts
2. A Google Cloud project with the People API enabled
3. OAuth 2.0 credentials for your Google Cloud project
4. A CSV file with contact information

## Setup Instructions

### 1. Create a Google Cloud Project

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Navigate to "APIs & Services" > "Library"
4. Search for "Google People API" and enable it

### 2. Create OAuth Credentials

1. In the Google Cloud Console, go to "APIs & Services" > "Credentials"
2. Click "Create Credentials" > "OAuth client ID"
3. Select "Desktop application" as the application type
4. Give it a name (e.g., "Google Contacts Sync")
5. Download the credentials JSON file
6. Rename the downloaded file to `credentials.json`

### 3. Add Test Users

If your Google Cloud project is in "External" user type:
1. Go to "APIs & Services" > "OAuth consent screen"
2. In the "Test users" section, add your Google account email
3. Save changes

### 4. Prepare Your CSV File

Your CSV file should include the following columns:
- First Name
- Middle Name
- Last Name
- Organization Name (this is used as the unique identifier)
- Organization Title
- E-mail 1 - Value
- Phone 1 - Value

**Note**: Only contacts with an Organization Name will be processed.

## Usage

1. Open the [Google Colab](https://colab.research.google.com/) website
2. Create a new notebook
3. Copy and paste the code from the provided script
4. Run the notebook
5. When prompted, upload your `credentials.json` file
6. Upload your CSV file when requested
7. Follow the authentication instructions to grant access to your Google Contacts
8. The script will process your contacts and show detailed logs

## How It Works

1. **Authentication**: The notebook uses OAuth 2.0 to authenticate with the Google People API, requesting the necessary scopes for Contacts access.

2. **CSV Processing**: The CSV file is read, and only rows with a valid Organization Name are processed.

3. **Contact Matching**: For each valid row, the script searches your Google Contacts for a matching Organization Name.

4. **Updating Contacts**: If a match is found, the script compares the CSV data with the existing contact data and only updates fields that have changed.

5. **Creating Contacts**: If no match is found, a new contact is created with the information from the CSV.

6. **Logging**: The script provides detailed logs showing exactly what was changed, created, or skipped.

## Features

- **Selective Updates**: Only fields that have changed are updated
- **Name Field Support**: Updates first, middle, and last names
- **Clean Phone Handling**: Prevents phone numbers from being converted to floating point format
- **Detailed Logging**: Clear logs with emoji indicators for different actions
- **Summary Statistics**: Count of contacts processed, updated, created, and failed

## Limitations

- The script assumes Organization Name is unique across your contacts
- Only basic contact fields are supported (name, email, phone, organization)
- No batch processing for very large CSV files (process one at a time)

## Troubleshooting

### Authentication Issues

If you encounter authentication errors:
1. Ensure the People API is enabled in your Google Cloud project
2. Verify you added your email as a test user in the OAuth consent screen
3. Delete any existing `token.pickle` file to force re-authentication
4. Make sure you're using the correct `credentials.json` file

### CSV Format Issues

If your contacts aren't being processed correctly:
1. Check that your CSV has the required columns
2. Ensure the Organization Name field is populated for contacts you want to process
3. Verify there are no encoding issues with your CSV file

## License

This project is licensed under the MIT License - feel free to modify and use it for your needs.

## Acknowledgments

- Google People API Documentation
- Google Colab Team




## Prompt
```text
I've been working on creating a Google Colab notebook that synchronizes contacts between a CSV file and Google Contacts. The solution identifies contacts by Organization Name (which is unique in our system) and performs updates or creates new contacts accordingly.
Key details:

CSV file structure: Has columns including First Name, Middle Name, Last Name, Organization Name, Organization Title, E-mail 1 - Value, and Phone 1 - Value.
Our CSV has 358 total rows but only 1 with an Organization Name field populated.
We're using the Google People API to interact with Google Contacts.
Authentication is done using OAuth with the proper Contacts API scope.
We successfully overcame several challenges including:

Authentication issues in Colab's environment
Adding proper scopes to access the Contacts API
Handling etags for contact updates
Preventing floating point conversion of phone numbers
Only updating contacts when values actually change
Handling all name fields (first, middle, last)



Current functionality:

The notebook authenticates with the Google People API
It reads the CSV, filtering for rows with an Organization Name
For each valid row, it checks if a contact with that Organization Name exists
If the contact exists, it updates fields that have changed (names, email, phone)
If the contact doesn't exist, it creates a new one
The process provides detailed logging showing exactly what's changed

We resolved various issues including:

Handling authentication in Colab (using out-of-band authorization)
Getting proper scopes for the Contacts API
Handling Google's etag requirements for updates
Preventing phone numbers from being converted to floats
Managing function parameter changes across code updates

Most recent code is fully functioning, and we've tested it with a CSV file containing one valid contact. I'd like to continue developing this solution by addressing additional features or refining the existing functionality.
Please help me build on this foundation by:

Suggesting improvements to make the code more robust
Adding batch processing capabilities for large CSV files
Enhancing the error handling and reporting
Adding support for additional contact fields like addresses or websites
```
