# Intro: projectfind / projectreplace
projectfind searches within and below the current working directory for a keyword or phrase and projectreplace replaces it with some other string. projectreplace uses projectfind and both can be used similarly. The available arguments and usages are the same between the two, but for the sake of clarity this guide is separated into one part for each. </br> </br>

If I'm handed an old python project without a requirements.txt, I might run `projectfind import` to find all the libraries needed for the project to run. 
Or if I'm working on an old project with some loose ends, I'll run `projectfind todo -i`. Similarly, if I want to rename a class, I would run `projectreplace className newName`. </br> </br>

It works on my debian install. If theres issues with it working on other platforms or shells, I might fix it. Open an issue to get it on my radar.

## projectfind
Finds all instances of a keyphrase within a project.

### Usage
projectfind [keyphrase] [arguments]</br>
projectfind expects a keyphrase followed by any additional arguments.</br>

### Arguments
-h, --help</br>
&emsp;Display the help manual.</br>
-d <val>, --depth <val></br>
&emsp;The number of directories deep a search should go. Default is 2.</br>
-e <val>, --exclude <val></br>
&emsp;Any file or directory glob that should be excluded from search.</br>
-i, --ignorecase</br>
&emsp;Case agnostic search.</br>
-p, --partial</br>
&emsp;Match keyphrase even if it is a part of another word.</br>
-r <filename>, --exclusionrules <filename></br>
&emsp;Takes a file containing a newline separated list as argument. Any files or directories matched by globs in the list are excluded from the search. Useful if you search a project a lot or have some common system wide paths you exclude often.

### Output
Returns a newline seperated list of file, line number, and line contents of each instance of the keyphrase across the project.

### Examples
`$projectfind import`</br>
&emsp;Finds all instances of "import" in files up to 2 directories below current working directory.</br>
`$projectfind main -d 1`</br>
&emsp;Finds all instances of "main" only in the current working directory.</br>
`$projectfind include -e Doxyfile -e bin/`</br>
&emsp;Finds all instances of "include" to depth 2, ignoring the bin directory and Doxyfile file.</br>
`$projectfind todo -i`</br>
&emsp;Case agnostic search for "todo".</br>
`$projectfind import -p`</br>
&emsp;Finds instances of "import" as well as other words like \"imported\".</br>
`$projectfind exec -r .gitignore`</br>
&emsp;Finds instances of "exec" excluding anything listed in .gitignore.</br>
`$projectfind \"todo|TODO\"`</br>
&emsp;Searches for instances of "todo" or "TODO".</br>
`$projectfind include \<time.h\>`</br>
`$projectfind include "<time.h>"`</br>
`$projectfind "include <time.h>"`</br>
&emsp;These all find any instance of "include <time.h>" across the project with depth 2.

## projectreplace
Replaces all instances of a phrase in a project with some other string.</br>
projectreplace is built off of projectfind. All arguments and examples here are similarly mirrored in projectfind.

### Usage 
projectreplace [keyphrase] [replace phrase] [arguments]</br>
projectreplace expects a keyphrase and the string to replace it with, followed by any additional arguments.</br>

### Arguments
-h, --help</br>
&emsp;Display this manual.</br>
-d <val>, --depth <val></br>
&emsp;The number of directories deep a search should go. Default is 2.</br>
-e <val>, --exclude <val></br>
&emsp;Any file or directory glob that should be excluded from search.</br>
-i, --ignorecase</br>
&emsp;Case agnostic search.</br>
-p, --partial</br>
&emsp;Match and replace keyphrase even if it is a part of another word.</br>
-r <filename>, --exclusionrules <filename></br>
&emsp;Takes a file containing a newline separated list as argument. Any files or directories matched by globs in the list are excluded from the search. Useful if you search a project a lot or have some common system wide paths you exclude often.</br>

### Output
Returns the content of each changed line in the project.</br>

### Examples
`$projectreplace import include`</br>
&emsp;Finds all instances of "import" in files up to 2 directories below current working directory and replaces it with "include".</br>
`$projectreplace main notMain -d 1`</br>
&emsp;Finds and replaces all instances of "main" with "notMain" only in the current working directory.</br>
`$projectreplace include import -e Doxyfile -e bin/`</br>
&emsp;Finds and replaces all instances of "include" with replace, except in the bin directory and Doxyfile file.</br>
`$projectreplace todo TODO -i`</br>
&emsp;Case agnostic search for "todo" and replace all with "TODO".</br>
`$projectreplace import Import -p`</br>
&emsp;Finds instances of "import" as well as other words like "imported" and replaces the matching part of the word with "Import".</br>
`$projectreplace exec run -r .gitignore`</br>
&emsp;Replaces instances of "exec" with "run", excluding anything listed in .gitignore.</br>
`$projectreplace "todo\|TODO" DONE`</br>
`$projectreplace "todo|TODO" DONE -E`</br>
&emsp;Replaces all "todo" and "TODO" with "DONE".</br>
`$projectreplace "include <time.h>" "include \"mytime.h\""`</br>
&emsp;Replace a string with whitespace and special characters.</br>
