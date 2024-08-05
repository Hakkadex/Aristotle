
Aristotle Tool
Aristotle is a simple Linux tool that fetches Wikipedia pages based on the subject you provide and displays them in your terminal.

Open a Terminal:

nano /path/to/your/directory/aristotle.py

Paste this Code into nano save and exit



#!/usr/bin/env python3

import sys
import requests

def get_wikipedia_page(subject):
    user_agent = 'Aristotle'  # Custom User-Agent
    url = f"https://en.wikipedia.org/w/api.php"
    params = {
        'action': 'query',
        'format': 'json',
        'titles': subject,
        'prop': 'extracts',
        'exintro': True
    }
    headers = {
        'User-Agent': user_agent
    }
    
    response = requests.get(url, headers=headers, params=params)
    data = response.json()
    pages = data.get('query', {}).get('pages', {})
    for page_id, page in pages.items():
        if page_id != '-1':
            print(f"Title: {page.get('title', 'No title available')}")
            print(f"Summary: {page.get('extract', 'No summary available')}")
        else:
            print(f"Page '{subject}' does not exist on Wikipedia.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: aristotleget <subject>")
        sys.exit(1)

    subject = " ".join(sys.argv[1:])
    print(f"Subject to search: {subject}")  # Debug statement
    get_wikipedia_page(subject)






Make the script executable with the following command:

chmod +x /path/to/your/directory/aristotle.py


Create a symbolic link to make the script accessible from anywhere in the terminal:

sudo ln -s /path/to/your/directory/aristotle.py /usr/local/bin/aristotleget


To use the tool, open your terminal and run:
aristotleget <subject>

Example Usage 
aristotleget Atlantis


Troubleshooting
Permission Denied:
Ensure that you have made the script executable and created the symbolic link correctly.

Script Not Found:
Double-check the path used in the symbolic link and ensure the script exists at that location.

Errors or No Output:
Verify that you have an active internet connection and the Wikipedia API is reachable.



