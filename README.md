# ASIS Content Generator

## Purpose
   1. To illustrate the operation of a simple Content Generater
   1. To require the student to complete the assignment within a defined timeframe

## Due Date: At the end of this lab section
  - This assignment is due at the end of this lab section
  - There will be *NO* acceptance of late work
  - Submit what you have accomplished, even if it is not complete, *before* the end of the lab.

## Assignment
  - You are to create a simple program, in a language of your choosing
  - The program generates a HTTP response from an 'asis' file.
  - The name of the 'asis' file is provided as the first input parameter to your program
  - The output file is provided via stdout.

### Examples:
  1. Valid Input file: filename.asis
  
     $ `cat filename.asis`
     ```
     status: 200 Cool
     X-hostname: cit384-${UID}.csun.edu
     content-type: text/plain

     A plain text file
     ```
     $ `./send-as-is filename.asis`
     ```
     HTTP/1.1 200 Cool
     server: premortal/cit-384/${UID} 
     date: ${DATE}
     X-hostname: cit384-${UID}.csun.edu
     content-type: text/plain

     A plain text file
     ```

  1. File not found:
   $ `cat no-such.asis`
     ```
     cat: no-such.asis: No such file or directory
     ```
     $ `./send-as-is no-such.asis`
     ```
     HTTP/1.1 400 Not found
     server: premortal/cit-384 
     date: ${DATE}
     
     ```

# Data file: the `asis` file
  1. The input file will be a text file with a file extention of .asis
  1. The input file has four components
     1. The HTTP response status line, which shall have the following syntax
        ```
        status: number "string" 
        ```
     1. A list of HTTP response header fields
     1. A blank line
     1. HTTP response body (optional)


# Output file:
  1. In general, the output file is a copy of the `asis` file, with the following changes
     1. The status field is transformed int the HTTP response line
        ```
        status: number "string"
        ```
        to
        ```
        HTTP/1.1 number "string"
        ```
     1. The following two headers fields are added to the output:
        - server: with the value of permortal/cit-384/${UID}
        - date:  the current date in which the output was generated


# Enhancements
  1. Create a log file call: `asis.access.log`
     - Record each time the asis program is executed.
  1. Create an error log file called: `asis.error.log`
     - If the data file does not exist, emit an appropriate message.
