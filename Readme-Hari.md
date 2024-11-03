in wsl   
git clone https://github.com/langchain-ai/langchain-academy.git    
cd langchain-academy   
python3 -m venv .venv    
source .venv/bin/activate   
pip install -r requirements.txt    
created .env and put all env variables    
create setenv   
cursor .   
at terminal jupyter notebook   
 

setenv file code  
```bash 
#!/bin/bash

# Check if a .env file exists in the current directory
if [[ -f .env ]]; then
  # Read each line in the .env file
  while IFS= read -r line || [ -n "$line" ]; do
    # Skip empty lines and comments
    if [[ -z "$line" || "$line" == \#* ]]; then
      continue
    fi
    # Export each variable and print its name and value
    export "$line"
    echo "Set $(echo "$line" | cut -d '=' -f 1) to $(echo "$line" | cut -d '=' -f 2-)"
  done < .env
  echo "Environment variables loaded from .env file"
else
  echo ".env file not found in the current directory"
fi


## Understanding syntext
IFS= read -r line

IFS=: This sets the Internal Field Separator (IFS) 
to an empty value for this command. Normally, 
IFS determines how Bash splits words during variable expansion. 
By setting IFS to empty, we ensure read does not trim leading/trailing 
whitespace or split the line on spaces or tabs.

read -r line:

read is used to read one line of input at a time.
-r prevents read from interpreting backslashes (\) as escape characters, 
which ensures that backslashes are read literally.
line is the variable that stores the current line from the .env file.

|| [ -n "$line" ]:

|| is a logical OR operator.
[ -n "$line" ] is a condition that checks if line is non-empty (-n means "non-zero length").
This part ensures the loop doesn’t terminate 
if the last line in the .env file lacks a newline character 
(which read could interpret as an end-of-file condition without reading the last line).

$(echo "$line" | cut -d '=' -f 1): 
Extracts the variable name by splitting line on = and taking the first field.

$(echo "$line" | cut -d '=' -f 2-): 
Extracts the variable value by taking everything after the first =.

```