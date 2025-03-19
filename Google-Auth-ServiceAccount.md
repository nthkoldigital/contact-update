# Service Account Setup for Google Contacts Sync

This guide will help you set up a service account with domain-wide delegation to access Google Contacts without requiring user interaction during authentication.

## Prerequisites

1. A Google Workspace (formerly G Suite) account with admin access
2. Access to the Google Cloud Console
3. The ability to create and manage service accounts

## Step 1: Create a Google Cloud Project

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Make note of your project ID as you'll need it later

## Step 2: Enable the Google People API

1. In your project, navigate to "APIs & Services" > "Library"
2. Search for "Google People API" and select it
3. Click "Enable" to activate the API for your project

## Step 3: Create a Service Account

1. Navigate to "APIs & Services" > "Credentials"
2. Click "Create Credentials" and select "Service account"
3. Enter a name for your service account (e.g., "Google Contacts Sync")
4. Optionally add a description
5. Click "Create and Continue"
6. Skip the "Grant this service account access to project" step (click "Continue")
7. Skip the "Grant users access to this service account" step (click "Done")
8. You should now see your service account in the list

## Step 4: Create and Download the Service Account Key

1. In the service accounts list, find the one you just created
2. Click the three dots in the "Actions" column and select "Manage keys"
3. Click "Add Key" > "Create new key"
4. Select "JSON" as the key type
5. Click "Create"
6. The key file will be automatically downloaded to your computer
7. Rename this file to `service-account.json` for use with the sync tool

## Step 5: Enable Domain-Wide Delegation

1. Return to the service accounts list
2. Click on your service account name to view its details
3. Click the "SHOW DOMAIN-WIDE DELEGATION" button
4. Check the "Enable Google Workspace Domain-wide Delegation" box
5. Provide a product name for the consent screen (e.g., "Contacts Sync")
6. Click "Save"
7. Note your service account's Client ID (a long number) for the next step

## Step 6: Configure Domain-Wide Delegation in Google Workspace

1. Go to your [Google Workspace Admin Console](https://admin.google.com/)
2. Navigate to "Security" > "API controls"
3. In the "Domain-wide Delegation" section, click "Manage Domain Wide Delegation"
4. Click "Add new"
5. In the "Client ID" field, enter your service account's Client ID
6. In the "OAuth Scopes" field, enter: `https://www.googleapis.com/auth/contacts`
7. Click "Authorize"

## Step 7: Make Note of the Admin or User Email

When running the sync tool, you'll need to provide the email address of a user to impersonate. This should be:

- A Google Workspace admin account, or
- A specific user account that has access to the contacts you want to manage

The service account will perform actions as this user, so make sure the user has the appropriate permissions to manage contacts.

## Step 8: Use with the Sync Tool

1. Upload the `service-account.json` file when prompted by the sync tool
2. When asked, enter the email address of the user to impersonate
3. The tool will authenticate using the service account without requiring any user interaction

## Troubleshooting

If you encounter authentication issues:

1. Verify the People API is enabled in your project
2. Check that the service account has domain-wide delegation enabled
3. Confirm the OAuth scope is correctly configured in the Google Workspace Admin Console
4. Ensure the user you're impersonating has the necessary permissions for contact management
5. Verify the service account JSON file is correctly formatted and contains all required fields
