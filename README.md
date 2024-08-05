Open a Terminal
nano /path/to/your/directory/aristotle.py
copy and paste source code into nano, save and exit nano
Make the script executable with the following command:
chmod +x /path/to/your/directory/aristotle.py
Create a symbolic link to make the script accessible from anywhere in the terminal
sudo ln -s /path/to/your/directory/aristotle.py /usr/local/bin/aristotleget
To use the tool type aristotleget <subject>
Example usage
aristotleget Atlantis
Your terminal will now explain to you what Atlantis is by pasting a wikipedia description inside the terminal
