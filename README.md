# contact-update

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
