Stata commands and names are case-sensitive.

## help

    * Open in the viewer window
    help command-name
    
    * Show in the Results window
    chelp command-name
    
    * built-in datasets
    sysuse dir
    
    * use one of the datasets
    sysuse name

## Some statistical functions

 - t: prob. on the left. 
 - ttail: prob. on the right 

	    t(df, n) + ttail(df, n) == 1

 - invt: t-value given prob. on the left
 - invttail: t-value given prob. on the right

	    invt(df, p) + invttail(df, p) == 0

## Describe

    * Description of the dataset and variables
    desc
    
    * List all notes
    notes
    
    * List notes of a variable
    notes var
    
    * Summarize mean, min, max, std, #obs of all vaiables 
    sum
    
    sum var1 var2
    
    * See what function you could use to get those values
    return list

## Operators

     ! not (also ~)
     | or
     & and
     != not equal (also ~=)

## Missing values

Stata lists missing values as a dot:

    list var1 var2 if missing(var2)

## New variables

    gen var2 = log(var1)  
    gen settingsq = setting^2
    
    quietly summarize setting
    gen settingcsq = (setting - r(mean))^2
    
    * generate new and delete old variable
    drop or use the replace option
    
    generate hieffort1 = effort > 14
    or
    generate hieffort2 = 0
    replace hieffort2 = 1 if effort > 14
    better:
    generate hieffort = effort > 14 if !missing(effort)
    
    gen effort5to14 = (effort >=5 & effort <= 14)

## Functions

    help mathfun
    
## Read data
    
    * Read data from excel
    help import excel
    
    * Read data from relational database
    help odbc
    
    * str14: country is a string of up to 14 chars
    infile str14 country setting effort change using [url]
    
    * Read data separated by commas or tabs
    help import delimited
    
    * Read data with each variable on a fixed position
    infix str country 4-17 setting 23-24 effort 31-32 change 40-41 using [url]
    
    * Read data with many variables, use a dictionary
    * Store the following into file.dct
    infix dictionary using url {
		str country 4-17
		setting 23-24
		effort 31-32
		change 40-41
	}
	
	infix using file.dct, clear
	or 
	infix using dictionaryfile, using(datafile) 
	
	* enter data manually
	help input

## Annotation

    label data "dedewdwedewd"
    
    notes: dwedewdwedew
    
    label variable var "dwedewdewd"
    
    notes varname: text
    
    generate effortg = effort
    * min or max
    recode effortg 0/4=1 5/14=2 15/max=3
    or

 - Values are assigned to the first category where they fall. Values that are never assigned to a category are kept as they are. You can use else (or *) as the last clause to refer to any value not yet assigned.
 - Alternatively, you can use missing and nonmissing to refer to unassigned missing and nonmissing values; these must be the last two clauses and cannot be combined with else.

dewdwed

    recode effort (0/4=1 Weak) (5/14=2 Moderate) (15/max=3 Strong), generate(efffortg) label(effortg)

    recode effort 0/4=1 5/14=2 15/max=3, gen(effortg)
    label define effortg 1 "Weak" 2 "Moderate" 3 "Strong", replace
    label values effortg effortg
    label variable effortg "Family Planning Effort (Grouped)"
    
    label define yesno 1 "yes" 0 "no"
    label values variablename yesno
    
    label dir (lists only names)
    label list (lists names and labels)
    
## Plot

    
    graph twoway scatter y x
    
    graph export scatter.png, width(500) replace
    
    graph twoway (scatter y x) (lfit y x)

## Other

    * regress using the first 2070 rows
    reg y x1 x2 x3 if _n <= 2070

    cd dir
    
    pwd
    
    log using filename, text replace
    
    log close
    
    do do-file
    
    * Break a long command into multiple lines
    /// 
    
    * Use ; to indicate end of a command
    #delimit ;
    
    * Change it back
    #delimit ;
    
    * Specify the version
    version 16
    
    * delete data and labels in memory
    clear
    
    * delete data and all saved results, scalars, and matrices
    clear all
    
    * Check the limits for stata
    help limits
    
    * see ranges of different datatypes
    help datatype
    
    * Find the most economic way to store data
    compress
    
    * string to numeric
    destring or real or encode
    
    * numeric to string
    tostring or decode
    
    * list data 1-3
    list in 1/3
    
    merge, append, joinby, cross
    
    
    
    

 - Variable names can have up to 32 chars

## Shortcut

    do editor: ctrl + 9 
    run do file: ctrl + D

## Missing values

    valid_numbers < . < .a < ... < .z.
    
    * Missing values
    var >= . or missing(var)
    
    There are different kinds of missing value codes
    * .n is not applicable
    replace ageAtMar = .n if ageAtMar == 88
    * .m is missing
    replace ageAtMar = .m if ageAtMar == 99

## Comments

    * at the start
    // comment what's after in the line
    /*  */ comment multiple lines (can be used in the middle of a line)


Get values of a regression:

    reg A B
    
    ereturn list
    
    * get estimates of coefficients
    display _b[var]
    * get standard error of coefficient
    display _se[var]


It is always a good idea to start every do file with comments that include at least a title, the name of the programmer who wrote the file, and the date. Assumptions about required files should also be noted.


## Exit
    
    
    * Save the data
    compress (for large datasets, compress before saving)
    save filename
    use filename
    
    exit
    
    * Exit and don't save the data
	    exit, clear