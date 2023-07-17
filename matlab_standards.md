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

