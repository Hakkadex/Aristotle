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
