# MATLAB Programming Standards

**STATUS:** This document is in development as of May 16th, 2023

**Scope:** This document details source code requirements and programming idioms required for all MATLAB code of the Accelerator Directorate, SLAC National Accelerator Laboratory. It additionally gives some recommended practices and examples.

**Purpose:** insert a fancy sentence about readability and such

# Naming Conventions

This section describes recommendations for naming conventions.

## Name Shadowing

**Description:** Functions and variables **MUST NOT** shadow Mathworks-shipped functionality or other code. This includes MATLAB files (.m, .p, .mlapp, .mlx), mex-files (.mexw32 etc.) and Simulink files (.mdl, .slx).

**Rationale:** Shadowing code can result in unexpected behaviour, because it is unclear and not properly defined for example what function is called when multiple ones share the same name.

## Units

**Description:** Variable names **MUST** be documented, either in the variable name, or as end-of-line comments in square brackets. Prefer end-of-line comments if addition to the variable name will make it excessively long.

**Rationale:** Maintain readability by using concise variable names.

DO:

	time_min = 2; 
	time_s = 120; 
	acceleration = 1000; % [mm/s^2] 
	
DON'T:

	time = 2; 
	accelerationInMillimetersPerSecondSquared = 1000;
	
	

## Negated Boolean Names

**Description:** Variable names **SHOULD NOT** include the word not.

**Rationale:** Readability decreases when variables have negated boolean names, especially in combination with the ~ operator.

DO:

	if isValid && ~isFound 
    	error('My error message.') 
	end 

DON'T:

	if ~notValid && isNotFound 
		error('My error message.') 
	end 
	
## Descriptive Names

**Description:** Names for functions, classes, packages and variables **MUST** be precise and descriptive.

**Rationale:** This increases the readability of the code.

DO:

	function tk = convC2k(temp)
	
DON'T:

	function temperatureK = convertCelsiusToKelvin(temperatureC) 
	
	
## The 'n' Prefix

**Description:** The prefix n **SHOULD** be used for variables that represent a number of things. The prefix **SHOULD NOT** be used for other purposes, and other prefixes for representing the number of things **SHOULD NOT**.

**Rationale:** Variables starting with this prefix can easily be identified.

DO:

	nFiles 
	nCars 
	nLines 
	
DON'T:

	numberOfFiles 
	nrCars 
	lineCount

## Name Length

**Description:** Variable names should be at most 32 characters long. Function names should be at least 3 and at most 32 characters long.

**Rationale:** Names shall be descriptive, so should not be too short. However, variable names can sometimes be single characters (x, y) and still be descriptive. Names that are too long can reduce readability because they introduce long lines of code.

DO:
	
	maxData = max(data); 
    

DON'T

    maximumValueOfTheEntireSetOfDataPoints = max(data);

## Loop Iterator Naming

**Description:** Iterator variable names **SHOULD** be at least 3 characters long. In nested for-loops, the starting letters of the iterator names **SHOULD** be subsequent letters in the alphabet.

**Rationale:** Iterator variables of for-loops are easily distinguishable from other variables by using these prefixes.

DO:

	for iNode = 1 : 10 
		for jPoint = 1 : 3 
       	myGraph(iNode).plotIt(jPoint); 
    	end 
	end 

DON'T:

	for nodeIdx = 1 : 10 
    	for j = 1 : 3 
       	myGraph(nodeIdx).plotIt(j); 
    	end 
	end   

## Parent / Child Name Redundancy

**Description:** Names of fields and properties **SHOULD NOT** contain their parent struct or object's name.

**Rationale:** When referenced, the fields and properties can have the same phrase multiple times in a row, which is unnecessary.

DO:

	Beam.thickness 
	chair.weight 

DON'T:

	Beam.beamThickness 
	chair.weightOfChair
	

## Names to Avoid

**Description:** Names of classes, functions, variables, properties and struct fields **SHOULD NOT** start with temp, my and they **SHOULD NOT** have names such as myClass, testFunction, etc.

**Rationale:** Names like these do not properly indicate what the class, function or variable is for.

In particular: 

	myClass 
	my_Class 
	TheClass 
	myFunction 
	myFunc 
	my_function 
	TheFunc 
	myVar 
	my_var 
	theVar 
	myProp 
	my_prop 
	temp 
	tmp 
	test 
	
## Function Names Document Their Use

**Description:** The names of functions **MUST** document their use.

**Rationale:** By choosing a clear and descriptive name, the code becomes more readable.

DO:

	model_rMatGet 
	control_bpmGet 
	util_gaussFit 
	gui_sliderControl  

DON'T:

	modelFunction 

## Function Name Construction

**Description:** Function names **SHOULD** consist of a verb (action) followed by a noun (direct object). For class methods, the direct object may be omitted if it is redundant. 

**Rationale:** This way it is more likely to be clear what the function does and if there is no suitable name following this guideline, (for example because the function does more than one thing) the function may have to be refactored.

DO:

	getPosition
	findOutlier
	multiplyNumbers
	updateModel
	getTwiss
	standardizeMagnet
	checkConvergence

DON'T:

	rMat 
	gauss 
	bpms 
	sliderstuff 


## Casing

TBD


## The 'is' Prefix

**Description:** The is prefix **SHOULD** be used for functions returning logical values or properties and variables holding logical values.

**Rationale:** This increases the readability of the code as it is clear from the name.


## Abbreviations

**Description:** Variable names **SHOULD NOT** contain abbreviations; except for idiomatic abbreviations commonly used at SLAC. (Found in SLAC Speak)

**Rationale:** Maintain readability by not abbreviating words in your variable names. Common acronyms are allowed.

DO:

	arrivalTime 
	bpmCharge 
 
COMMON EXCEPTIONS: 

	bpm 
	toro 
	xcor 
	ycor 
	bdes 
	
DON'T:

	arrTim 
	bpmC
	
	
## The 'Test' Suffix

**Description:** The suffix "Test" **SHOULD** only be used for unit test filenames.

**Rationale:** This increases the readability of the code as it is clear from the name of the file that it is a unit test file.

# Layouts and Comments

This section describes recommendations for code layout and comments.

## Comment Blocks

**Description:** Comment blocks **SHOULD NOT** be used.

**Rationale:** Consistent comment syntax improves readability.

DO:

	% This is a comment. 
	% This is also a comment. 

DON'T:

	%{ This is a comment. 
	This is also a comment. 
	%}

## Function Indentation

**Description:** Functions **SHOULD** be indented on the root level of a file.

**Rationale:** Consistent indentation improves readability.

DO: 

	function computeWeight(in) 
   		weight = 2 * in; 
	end 

DON'T:

	function computeWeight(in) 
	weight = 2 * in; 
	end 

 ## Whitespace in Statements

 **Description:** The following operators **SHOULD** be surrounded with spaces: 
= : ^ == <= >= < > ~= & &&  | ||  + - * .* /  
A space **SHOULD NOT** be used between the unary minus-sign and its operand. 

**Rationale:** Whitespace around operators often leads to improved readability. As an exception, do not use spaces around the equals signs when using the Name=Value syntax introduced in MATLAB R2021a. 

DO:

	isValid = (y > 0) && (x == -1); 
 
DON'T:

	isValid=(y>0)&&(x==-1);

## Whitespace in Characters

**Description:** Commas, semicolons and keywords (for, while, if etc.) **SHOULD** be followed by a space unless at the end of the statement. 

**Rationale:** A clear separation of keywords from other code improves readability. 

DO:

	while ismember(x, [3, 5, 7, 11, 13]) 
    		x = x + 2; 
	end
 
DON'T

	while(ismember(x, [3,5,7,11,13])) 
	    x = x + 2; 
	end
 
## Line Length

**Description:** Lines **SHOULD** be no more than 120 characters long, including comments. When possible, keep lines shorter than 80 chracters long. 

**Rationale:** A line of code should fit on a screen. Long lines of code are difficult to interpret and generally indicate great complexity.

DO:

	theText = ['Lorem ipsum dolor sit amet, consectetur adipiscing elit. ', ... 
	            'Ut luctus arcu ex, at viverra nibh malesuada ac. Proin vel arcu leo.']; 

DON'T

	theText = 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut luctus arcu ex, at viverra nibh malesuada ac. Proin vel arcu leo.';

## Indentation Length

**Description:** Indentation **SHOULD** be four spaces long. This is the default setting in the MATLAB editor. 

**Rationale:** Using an adequate and consistent number of spaces for indentation improves readability and prevents unnecessary changes when others work on the code. 

DO:

	if x > 0 
	    if x < 2 
	        disp(x) 
	    end 
	end 

DON'T

	if x > 0 
	 if x < 2 
	   disp(x) 
	 end 
	end

## Comments on Poorly Written Code

**Description:** Comments **SHOULD NOT** be used to justify or mock poorly written code. Write proper code that requires no justification instead. 

**Rationale:** Readability will be improved if issues with the code are fixed immediately instead of documented in the comments. 

DO:

	x = 2; 
	y = 3 * x + z;  
	 
	z = [1, 23, 8.1] * (x ^ 3.1415) * sqrt(y); 

DON'T

	x = 2; 
	 
	% FIXME: This piece of ugly code is copied from StackExchange. 
	z=[1,23,8.1]*(x^3.1415)*sqrt(y);

## Commas in Rows

**Description:** Commas **SHOULD** be used to separate elements in a row. Place the comma directly after the element. 

**Rationale:** This improves readability, especially in arrays of strings or character vectors. 

DO: 

	fig.Position    = [0, 1000, 1.5, 130]; 
	saying          = ['An apple a ', period, ' keeps the doctor away.']; 
 
DON'T: 

	fig.Position    = [0 1000 1.5 130]; 
	saying          = ['An apple a ' period ' keeps the doctor away.']; 

## Line Continuation with Operators

**Description:** Binary operators **SHOULD** be placed in multi-line statements at the start and not at the end of the line. 

**Rationale:** By placing binary operators at the start of the line, it is immediately clear what the line does. 

DO: 

	isDone = isImplemented ... 
	    && isTested ... 
	    && isDocumented; 
     
DON'T: 

	isDone = isImplemented && ... 
	    isTested && ... 
	    isDocumented; 

## Methods/Properties Blocks with Duplicate Attributes

**Description:** Multiple properties and methods blocks with equal attribute values **SHOULD** be combined into one. Do not set attributes to their default values. 

**Rationale:** Having multiple blocks with the same attributes is unnecessary and decreases the readability of classdef files. 

DON'T

	classdef Rocket 
	    properties (Access = public, Hidden = false, Constant) 
	        Fuel = "Nuclear" 
	    end 
	     
	    properties (Constant = true) 
	        Capacity = 2 
	    end 
	end

DO

	classdef Rocket 
	    properties (Constant) 
	        Fuel = "Nuclear" 
	        Capacity = 2 
	    end 
	end 
 
## Whitespace at the End of a Line

**Description:** White space **SHOULD NOT** be used at the end of a line of code unless it is followed by a comment. 

**Rationale:** This prevents smart-indenting a file from inducing changes to those lines. 

## Help Text

**Description:** Header comments **SHOULD** be written with text markup to provide user documentation useful both in-file and when using the help and lookfor functions.

**Rationale:** This increases readability, and makes the code more likely to be found and less likely to be reinvented. 

DO:

	LINK TO HEADER EXAMPLE

DON'T:

	function [avg, maxSize] = measureSize(obj, dim) 
		avg = mean(obj.Size, dim); 
		maxSize = max(obj.Size, dim); 
	end
 
## Whitespace Around Blocks of Code

**Description:** Coherent blocks of code **SHOULD** be separated by one or more blank lines. 

**Rationale:** Increases the readability of the code. 

DO:

	% Shift to origin. 
	deltaX = mean(xIn); 
	xOutc = xIn - deltaX; 
	 
	% Calculate scaling. 
	scalingFactor = newZ / currentZ; 
	xOut = xOut .* scalingFactor; 
	 
	% Shift back. 
	xOut = xOut + deltaX; 

DON'T

	deltaX = mean(xIn); 
	xOut = xIn - deltaX; 
	scalingFactor = newZ / currentZ; 
	xOut = xOut .* scalingFactor; 
	xOut = xOut + deltaX;

## Correct Spelling

**Description:** Correct spelling and punctuation **SHOULD** be used in comments. Write in complete sentences, starting with a capital letter and ending in a period. 

**Rationale:** This increases the readability of code. Error-strewn and poorly constructed comments reflect on the code they accompany. 

DO:

	% Get the scaling factor. 
	scalingFactor = newZ / currentZ; 
	xOut = xOut * scalingFactor; % Now rescaled.  

DON'T:

	% get sclaing factor 
	scaling_factor = new_z / current_z; 
	x_out = x_out * scaling_factor; % now recslaed


## Align Struct Definition

**Description:** When defining a struct, thenames and values of the struct fields **SHOULD** be aligned. 

**Rationale:** This improves readability of the code by making it clearer what fields are defined and by what values. 

DO:

	s = struct(... 
	    "name",     "Albert", ... 
	    "age",      2021 - 1979, ... 
	    "isValid",  ismember("Albert", allNames)) 
     
DON'T:

	s = struct("name", "Albert", "age", 2021 - 1979, "isValid", ismember("Albert", allNames)); 


# Statements and Expressions

## Constant Definitions

**Description:** Constant definitions **SHOULD** be placed at the top of the function, after defining global/persistent variables. For classes, constant definitions **SHOULD** exist in a separate file.

**Rationale:** Consistent constant definition allows for easy identification.

DO:

	function testConstants(x) 
		MAX_Z = 100; 
		 
		y = 3 * x; 
		z = min(y, MAX_Z); 
	end 
 
DON'T:

	function testConstants(x) 
		y = 3 * x; 
		MAX_Z = 100; 
		z = min(y, MAX_Z); 
	end

## Magic Numbers

**Description:** Magic numbers **SHOULD NOT** be used in expressions. Define them as variables constants before using them. 

**Rationale:** This encourages reuse and documentation of numerical constants and improves overall readability.

DO:

	DECK_SIZE   = 52; 
	N_VALUES    = 13; 
	 
	for iPick = 1 : DECK_SIZE 
	    disp(randi(N_VALUES)); 
	end 

DON'T:

	for iPick = 1 : 52 
	    disp(randi(13)); 
	end 
 
## Function Calls Without Inputs

**Description:** Empty parentheses **SHOULD** be used for function calls without input arguments. 

**Rationale:** This helps to emphasize the fact that they are function calls and not variables or properties. 

DO:

	x = rand() * 2; 

DON'T:

	x = rand * 2;

## One Statement Per Line

**Description:** Each line **SHOULD** have at most one statement

**Rationale:** Maintain readability of your code by having each line of code do exactly one thing. 

**Exception:** One may declare a maximum of three variables on a single line if they are all of the same type or unit. One may place an if, for or while statement on one line if there is exactly one statement inside of the loop. 

DO:

	for iNode = 1 : 3 
	    x = x + iNode; 
	    disp(x); 
	end 
	 
	a = 1;  % Unitless 
	b = 2;  % Unitless 
	c = 3; % Unitless 
	disp(a + b + c); 
	 
	time_limit = 2; % [minutes] 
	time_start = 4; % [seconds] 
	time_stop = 9; % [seconds] 
	time_elapsed = time_stop - time_start; 

DON'T:

	for iNode = 1 : 3, x = x + iNode; disp(x); end 
	 
	a = 1;  % Unitless 
	b = 2;  % Unitless 
	c = 3; % Unitless 
	disp(a + b + c); 
	 
	time_limit = 2; % [minutes] 
	time_start = 4; % [seconds] 
	time_stop = 9; % [seconds] 
	time_elapsed = time_stop - time_start; 

EXCEPTIONS:

	% Variable declarations:
	persistent x, y; 
	 
	[a, b, c] = deal(1, 2, 3); 
	disp(a + b + c); 
	 
	time_limit = 2; % [minutes] 
	[time_start, time_stop] = deal(4, 9); % [seconds] 
	time_elapsed = time_stop - time_start; 
	 
	% One line loop: 
	for iNode = 1 : 3, x = x + iNode; end  % 1 statement inside loop is allowed 
 
## If/Else

**Description:** Every if **SHOULD** have an else section, even if it does not contain executable code. 

**Rationale:** By including an else section, no execution paths are overlooked. Additionally, code coverage can be accurately reported because without else, it is unclear whether the if-condition is ever false. 

DO:

	if x > 0 
	    saveData() 
	else 
	    % x does not indicate we want to save the dataset. 
	end 

DON'T:

	if x > 0 
	    saveData() 
	end

## Switch Otherwise

**Description:** Every switch **SHOULD** have an otherwise section, even if it does not contain executable code. 

**Rationale:** By including an otherwise section, no execution paths are overlooked. Additionally, code coverage can be accurately reported because without otherwise, it is unclear whether it happens that none of the cases occur. 

DO:

	switch reply 
	    case "Yes" 
	        saveData() 
	    case "No" 
	        clearData() 
	    otherwise 
	        % Should not get here. 
	        error("Unknown reply " + reply) 
	end 

DON'T:

	switch reply 
	    case "Yes" 
	        saveData() 
	    case "No" 
	        clearData() 
	end

## Mixed Types in Expressions

**Description:** Multiple operand types **SHOULD NOT** be used in a single operator. For example, do not mix logical and numerical operatonds with a multiplication operator. 

**Rationale:** Mixing operand types per operator can cause unexpected results and may lead to errors in case of true incompatibilities. 

DO:

	d = (a * b > 0) && c; 
 
DON'T:

	d = a * b && c;

## Parentheses in Logical Expressions

**Description:** Parentheses **SHOULD** be used to clarify the precedence of operands in expressions with multiple logical operators. No parentheses are required when only one type of logical operator is used. For example: d = a && b && c;. 

**Rationale:** By clarifying the precedence of the operands in such expressions, readability is improved and unexpected behaviour is prevented. 

DO:

	d = a && b || c;
 
DON'T:

	d = (a && b) || c; 

## Parentheses in Mathematical Expressions

**Description:** Parentheses **SHOULD** be used to clarify the precedence of operands in expressions with multiple mathematical operators. No parentheses are required when only one type of mathematical operator is used. For example: d = a * b * c;. 

**Rationale:** By clarifying the precedence of the operands in such expressions, readability is improved and unexpected behaviour is prevented. 

DO:

	d = (a * b) + c; 
	h = (f / 2) * g; 
 
DON'T:

	d = a * b + c; 
	h = f / 2 * g;

## Assert Inputs

**Description:**

**Rationale:**

## Global Variables

**Description:** The global keyword **SHOULD NOT** not be used. 

**Rationale:** The value of global variables can change from anywhere, which can make things unnecessarily complicated.

## Constant Conditional Statements

**Description:** Cconditions that are always true or always false, such as if true or elseif 0, **SHOULD NOT** be used. MATLAB's Code Analyzer warns about some of these cases. 

**Rationale:** These constructs may cause unreachable code or unintended behaviour. 

DO:

	disp(x)
DON'T:

	if x > 0 || true 
	    disp(x) 
	end    

## Group Struct Field Definitions

**Description:** All fields of a struct **SHOULD** be defined in a single, contiguous block of code. No fields should be added to a struct after using it. 

**Rationale:** Lines of code or functions using the struct might assume that all fields are already there, resulting in an error if the field is not there. 

DO:

	s = struct("f", 2, "g", 3, "h", 'new field'); 
	 
	computeCost(s); 
 
DON'T:

	s = struct("f", 2, "g", 3); 
	 
	computeCost(s); 
	s.h = 'new field'; 
 
## Eval Functions

**Description:** The built-in eval function **SHOULD NOT** be used. Use of feval, evalin and evalc **SHOULD** be minimized.

**Rationale:** These functions can have harmful results and statements using them are usually difficult to read and maintain. 
Additionally, it may be overlooked when variables are defined or altered by calls to these functions.

## Keywords Break, Continue, and Return

**Description:** Use the keywords break, continue and return **SHOULD** be avoided. 

**Rationale:** Using break, continue or return decreases readability because the end of the function is not always reached. By avoiding these keywords, the flow of the code remains clear. However, these keywords can be useful to reduce complexity and improve performance. 

DO:

	if isempty(x) 
	    % No further actions. 
	else 
	    <rest of the code> 
	end  

DON'T:

	if isempty(x) 
	    return 
	end 
	 
	<rest of the code>

## Shell Escape

**Description:** The shell escape function **SHOULD NOT** be used. If necessary, use the system function instead. 

**Rationale:** When using the !program_to_execute syntax to execute external programs, no dynamic input or program names can be used. 

DO:

	system('mycommand') 
 
DON'T:

	!mycommand 

## Dependencies Known

**Description:**

**Rationale:**

## Try/For Exception Handling

**Description:** The try construct **SHOULD** only be used for exception handling. An exception object must be assigned or created and an error function must be called in the catch. Do not use try/catch to suppress errors or to express simple conditions. There are other, more suitable options for that. 

**Rationale:** Using try for simple error suppression can result in poor performance and unexpected behaviour. When a different error occurs than the one expected, it can go undetected because of the try/catch. 

DO:

	if isfield(container, 'nElements') 
	    nElems = container.nElements; 
	else 
	    nElems = 0; 
	end 
 
DON'T:

	try 
	    nElems = container.nElements; 
	catch 
	    nElems = 0; 
	end

## Floaitng-Point Comparisons

**Description:** Floating-point values **SHOULD NOT** be compared using == or ~=. Use a tolerance instead. 

**Rationale:** Rounding errors due to algorithm design or machine precision can cause unexpected inequalities. 

DO:

	out = abs(myFcn(in) - sqrt(3)) < 1e-12; 
DON'T:

	out = myFcn(in) == sqrt(3);
 
## Workspace Variable Ans

**Description:** The workspace variable ans **SHOULD NOT** be used.

**Rationale:** Use of the workspace variable ans reduces the robustness and security of the code. 

## Debugging Functions

**Description:** Debugging functions such as dbstep, dbcont, dbquit, keyboardor other functions that interact with the MATLAB debugger **SHOULD NOT** be used within a script. 

**Rationale:** These functions that interact with the MATLAB debugger reduce the robustness of the code. 

## Logical Indexing

**Description:** Logical indexing **SHOULD** be used instead of linear or subscript indexing where possible.

**Rationale:** Logical indexing is faster and more readable. 

DO:

	index = (v > MIN) & (v < MAX); 
 
DON'T

	index = intersect(find(v > MIN), find(v < MAX));
 
## Loop Vectorization

**Description:** Vectorization **SHOULD** be used to apply operations to arrays where feasible.

**Rationale:** Vectorized loops are faster, more robust, more readable, and more maintainable. 

DO:

	dataResult = dataset < limit; 
 
DON'T:

	dataResult = false(size(dataset)); 
	 
	for iElem = 1 : numel(dataset) 
	    if dataset(iElem) < limit(iElem) 
	        dataResult(iElem) = true; 
	    else 
	        dataResult(iElem) = false; 
	    end 
	end

## Zero Before Decimal Point

**Description:** A zero before the decimal point **SHOULD** be used in numeric expressions. 

**Rationale:** Increases the readability of the code. 

DO:

	THRESHOLD = 0.5;
DON'T:

	THRESHOLD = .5;

## Accessing Other Workspaces

**Description:** Functions accessing workspaces outside the scope of the current function, such as assignin, evalin, clc, **SHOULD NOT** be used within scripts. 

**Rationale:** These functions reduce the portability, robustness and readability of the code. 

## Use Switch Blocks

**Description:** A switch block **SHOULD** be used instead of many if-elseif-else statements when possible. 

**Rationale:** The notation of a switch block is more concise and therefore, more readable and easier to maintain. 

DO:

	switch name 
	    case "Bill" 
	        ... 
	    case {"Judith", "Bob"} 
	        ... 
	    case "Steve" 
	        ... 
	    otherwise 
	        ... 
	end 

DON'T:

	if name == "Bill" 
	    ... 
	elseif ismember(name, ["Judith", "Bob"]) 
	    ... 
	elseif name == "Steve" 
	    ... 
	else 
	    ... 
	end

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

##

**Description:**

**Rationale:**

