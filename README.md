fit-extract (Data Extraction for EC-LAB)
================================================
Extracts parameter (R2, R3, Q1, etc.) data from all '.fit' files in
a specified folder and writes the extracted data into a 'Data.xlsx' in the
same folder. '.fit' files are created by clicking save in the EC-LAB software
after fitting (minimizing) a curve with Zfit. If data from multiple channels
is in the same folder, then the data will be separated into different sheets
in the same "Data.xlsv" file.

Requires python 3.2.x or above and pandas (should install automatically).


INSTALL
-----
Run from the command line:
    
    $ pip install fit-extract

Alternatively, you can download the zip from github or use git clone.


USAGE
-----
Navigate to the folder containing the .fit files using the command line:

    $ cd [FOLDERPATH]
    $ python fit-extract [OPTIONS]

Running with no options will run the program in the current directory. By default 
the program will extract R2 and R3 and group the lower values and higher value of 
each pair into the same column to ensure consistency. R1 should be set to 0.1 ohm 
in EC-Lab.

#### Important Usage Notes: 

Do not change the file name of any of the files. This program requires that the file name end in the default channel number format to work. This also helps with sorting (done lexicographically)

When working with data that has cycles, you must use the cycles (-c, see below) option. 
Also when saving your data in EC-Lab, do not click save multiple time for the same cycle. 
This will mess up how the program extracts cycles and create extra cycles for each time you 
do this. You can also just use the select all cycles option (randomize only on first cycle) in
EC-Lab to avoid this risk and usually works fine if your results are clean. If you are not using 
the cycles option, the most recent or latest save value so you are free to click save multiple times.

#### Arguments and Options:

**Help (--help or -h)**

    $ fit-extract -h
    
Displays usage information.

**Folder (--folder or -f)**

    $ fit-extract -f [FOLDERPATH [FOLDERPATH...]]

Runs the program in the specified folders (multiple can be specified). 
The path must be in quotes.

**Cycles (--cycle or -c)**

    $ fit-extract -c

If your data has cycles or loops, you will need to apply this option.

**Additional (--additional_parameters or -ap)**

    $ fit-extract -ap [PARAM [PARAM...]]

In additional to the default parameters extracted (R2, R3), the program will
also extract extra specfied parameters (Ex: Q2, a1). Note case matters.

**Custom (--custom_parameters or -cp)**

    $ fit-extract -cp [PARAM [PARAM...]]

Extracts specified parameters intead of default (R2, R3). Disables group by size unless added manually.

**Group By Size (--groupbysize or -gs)**
    
    $ fit-extract -gs [PARAM_1 PARAM_2]

Ensures consistency between two of the same type of parameter (default: R2, R3) 
by grouping their values by size.



#### Example:

    $ fit-extract -f 'C:\Users\[USER_NAME]\[PATH]' 'C:\Users\[USER_NAME]\[PATH2]' -ls -ap Q2 a1
    
Result - Data.xlsx file created in both paths specified with following information:

    Sheet Name: Ch 7

    File Name | R2 (ohm)           | R3 (ohm)         | Q2 (F.s^(a-1)) | a1 ()
    -------------------------------------------------------------------------------
    file.fit  | 12345              | 29929            | .00000023      | 0.124
    ...       | ...                | ...              | ...            | ...

    Additional Sheets: Ch 8, Ch 9


TODO
-----
- Update example.
- Better README / additional docs and images