# Statistics retrieval
This folder contains scripts that can be utilized to retrieve information about web applications modified by different analysis tools.



## Process
The process contains several steps, which must be ran *in order*, without duplicates.
Several steps modify the application irreversably, so *make a backup* before you start.


## Note on pre-processed data
If you already have pre-processed (e.g. https://github.com/NielsGrootObbink/jdce-thesis-data) data, simply copy `list.txt` and the `processed` directory to this directory.
Then run step 0 and then step 5 (skip step 1, 2, 3 and 4).




## Usage

### 0. Install required packages
Run `npm install` in the following folders:

+ `add_logs/`
+ `get_all/`



### 1. Setup
Create a folder named _processed_.
For each application, create a folder in the _processed_ folder (e.g. _processed/my-app/_)
In this folder, add the different versions, modified by analyzers (e.g. _processed/my-app/original/_, _processed/my-app/static/_, _processed/my-app/dynamic/_).


### 2. Modify scripts
Edit the following files (see line number suggestions) so they are correct for your analysis setup:

+ `./add_logs.js` line *45*
+ `./remove_duplicates.js` line *40*
+ `./statistics.js` line *21*
+ `list.txt`, each line should contain the folder name (app name) you wish to retrieve statistics for


### 3. Run base scripts
Run
```
node ./add_logs.js
node ./get_all.js
```
This creates the file _all.txt_ in each application folder.


### 4. Test applications by hand
Now, open and test functionality with each application type. After you have done so, open the console, and enter
```
var w=window.open('');w.document.write("<pre>" + ___jdce_logger_safe.join('\n') + "<pre>");
```
This should open a new window with a list of function calls. Copy output from new screen to a file with the name of the analyzer type (e.g. for _dynamic_, the file is _processed/my-app/dynamic.txt_).
This name should correspond to the folder name of the app analysis version you just tested.



### 5. Retrieve statistics
Run
```
node remove_duplicates.js
node statistics.js <type>
```
This should output a LaTeX table (for analysis type _type_) for each entry in the `list.txt` file.
