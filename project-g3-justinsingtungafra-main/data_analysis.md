# Determining Details
This file answers the following questions regarding the given dataset:

* What unknown wrong data is there
* How wrong/unknown data will be handled
* How Paris data will be encorporated into data file (how id's  will be generated, how duplicates will be determined, etc.)

## Q1 - Unknown/Wrong Data

athletes.csv
* name_tv is blank for some entries
* nationality and nationality_blank is blank for some entries
* height and weight are equal to 0 for some entries
* birth_date format is mm/dd/yyyy, should be dd-mon-yyyy
* some atheletes have blank entries for birth_place, birth_country, residence_place, residence_country

events.cvs
* multiple incomplete event values, ie. some of the events will be called just "men" or "women"

medallists.csv
* some athletes have blank team, team_gender, and code_team values

teams.csv
* some teams have blanks for events, coaches_codes, num_coaches

## Q2 - Handling Unexpected Data
Some of the values may not be required to be added to the new olympic files. They can be left blank. Values that need cleaning for the new olympic files will be explained below 

athletes.csv
* height and weight values that are 0 can be converted to null
* birth_date should be reformated by checking the format. If it is mm/dd/yyyy (check if the first value is less or equal to 12 and assume that it's in mm/dd/yyyy format if it is), then it should be converted to dd/mm/yyyy and then dd-mon-yyyy by extracting the day and year value from the date and then matching the number to its correct month. If year is given (check for four digit value) leave as is, otherwise make birth_date empty.

events.cvs
* Check if the event value just contain "Men" and "Women". If they do, change to "<sport value>, <Men/Women>" otherwise leave as is. Other incomplete values can be matched by finding keywords for the events.

## Q3 - Data Incorporation

### New Files
A copy of all the existing files should be created with "new_" at the front. For example, olympic_athlete_bio.csv will have a copy called new_olympic_athlete_bio.csv. This is so we can make sure the we still have the original files. 

### Comparing Entries
Before generating ID, we can check for duplicates by comparing athletes.csv and olympic_athlete_bio.csv. This can be done by comparing the name values, "born" values and country values. If there is a match in olympic_athelete_bio.csv found, new data will not be entered, but if it is we can go ahead and put a new entry. 

### Generating IDs
A simple way to generate an ID is to take the first 6-digits of the code value from the atheletes.csv and check if it exists in olympic_athlete_bio.csv. If it already exists, the program should randomly generate a new 6-digit ID and check if that exists in olympic_athlete_bio.csv. This part continues until the program comes up with a unique number.

### Formatting
The program should check that the information gathered in the right format before insertion. For example, it should take the name value from athlete.csv and turn the first name so that it follows the noun format (Firstname Lastname), the country, gender, height, weight and birth_date values (weight, height, birth_date will also be reformatted as explained in Q2) from athletes.csv for the country, sex, height, weight and born values in olympic_athelete_bio.csv. country_noc can be found by comparing country to its respective noc value in noc.csv. Once it verifies that everything is in the right format, it will then insert the new data into the file.
