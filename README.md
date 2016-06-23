# SingleWordSearch

# Purpose
Read from 2 column excel file = Column 1=Replace Term; Column 2=Search Term
Copy this data into Notepad++ and search it


# References

### Use virtualenv to activate the desired virtual environment
#### on macOS
Supply path to SingleWordSearch, e.g.

    source ./SingleWordSearch/venv/bin/activate

#### on Windows
    venv\Scripts\activate

### cd to project root directory

    cd SingleWordSearch

### download web pages

    python ./SingleWordSearch/download_web.py

### Search files and write search results to file
Search is similar to Unix/Linux grep command

#### specify argument values
Note: Suggest use different values for download_directory and results file directory.

Otherwise subsequent searches might accidentally search a results file.

    python ./SingleWordSearch/search_web.py -expression "ython" -search_directory "./SingleWordSearch_data/downloads" -out_dir "./SingleWordSearch_data/results" -out_file "SingleWordSearch_results.txt"

#### to use default argument values
    python ./SingleWordSearch/search_web.py

### get suggested spellings
Don't commit actual input file.
In .gitignore ignored oovwords.csv

    python ./SingleWordSearch/get_suggested_spellings.py -in_dir "./SingleWordSearch_data/inputs" -in_file "oovwords.csv" -out_dir "./SingleWordSearch_data/results" -out_file "suggested_spelling_results.csv"

#### to use default argument values
    python ./SingleWordSearch/get_suggested_spellings.py

## to concatenate regexes
    python3 ./SingleWordSearch/concatenate_regex.py

## Unit tests
To run tests, open terminal shell.  
cd to project directory. Run tests via python command or bash script.

### Bash script
Runs all test modules.  
Works on OS X. On Windows may work with Cygwin, I don't know.

    $ ./bin/run_tests

### python command
This command lists and tests all modules except web_downloader_arg_reader and web_searcher_arg_reader.

    python -m unittest tests.test_page_reader tests.test_file_writer tests.test_web_downloader tests.test_web_searcher

#### arg_reader tests
Attempting to run test_web_downloader_arg_reader and test_web_searcher_arg_reader has problem with arguments for unittest and for argparse.  
e.g. python -m unittest discover says "unrecognized arguments: discover" and wants the argparse arguments.  
TODO: Consider alternative solutions.  
http://stackoverflow.com/questions/35270177/passing-arguments-for-argparse-with-unittest-discover

---

## Download web page containing HTML and Javascript
Many web requests return a combination of HTML and Javascript.
For example, a google search.

        https://www.google.com/#q=javascwipt

In these cases, we can use a webbrowser to run the javascript and get more html.

http://stackoverflow.com/questions/11331071/get-class-name-and-contents-using-beautiful-soup
https://www.crummy.com/software/BeautifulSoup/bs4/doc/#searching-by-css-class

use class_ not Python keyword class

## oovlist.csv
File from Windows had line endings that show as ^M in vim.
Changed to Unix line endings.
http://stackoverflow.com/questions/811193/how-to-convert-the-m-linebreak-to-normal-linebreak-in-a-file-opened-in-vim
at vim command line type as below, including ^V and ^M

    :%s/<Ctrl-V><Ctrl-M>/\r/g

---

## Appendix virtual environment venv

The project uses a virtual environment.

https://docs.python.org/3/library/venv.html

This can hold a python version and pip installed packages such as "requests".

https://github.com/kennethreitz/requests

### Install virtual environment in directory named "venv"

    $ cd <project root directory>
    $ pyvenv venv

### Before activating virtual environment

On my machine, active python is 2.7.11

    ➜  SingleWordSearch git:(master) ✗ which python
    /usr/local/bin/python
    ➜  SingleWordSearch git:(master) python --version
    Python 2.7.11

On my machine, to use python3 must specify python3

    ➜  SingleWordSearch git:(master) which python3
    /usr/local/bin/python3

### Activate virtual environment

    ➜  SingleWordSearch git:(master) source ./venv/bin/activate

### Now active python is in venv and is version 3.5.1

Notice command prompt shows venv is active

    (venv) ➜  SingleWordSearch git:(master) which python
    /Users/stevebaker/Documents/projects/pythonProjects/SingleWordSearch/venv/bin/python
    (venv) ➜  SingleWordSearch git:(master) python --version
    Python 3.5.1


### Deactivate virtual environment
In shell run deactivate
    (venv) ➜  SingleWordSearch git:(master) ✗ deactivate

## Appendix upgrade pip
With virtualenv active

    pip install --upgrade pip

    Successfully uninstalled pip-8.1.0
    Successfully installed pip-8.1.2

Installed to project venv

## Appendix pip install dependencies
With virtualenv active

    pip install Npp

## Appendix clone app from github to another machine
After cloning app from github, activating venv did still showed system python.
Fixed as follows:

    delete ./venv
    Re-run pyvenv venv
    pip re-install packages.
