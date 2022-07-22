# PythonFile_I-O
 
What is file I/O?

    File I/O (File Input Output) is the manner in which we let our programs
    input something from the outside world, and output something back.
    
    Imagine we want to create an image compression program. We will require 
    I/O to accomplish this. We need file input to get the image, and we need
    file output to return the compressed image.
    
    Reading and writing files is an extremely important technique to know in
    programming. We fortunately have built in functions in Python to accomplish
    these tasks, ex:
    
    Imagine you have a text file called "test.txt", to use it in your program,
    you could do the following:
    
    my_file = open('test.txt')
    
    print(my_file.read())
    ^This will print the contents of the text file to the console. It will also
    move the cursor to the end of the file, so if you follow up with another
    print statement, you will read EOF (end of file) and will not print any
    thing to the screen. To combat that, you can include the following:
    
    .seek([index])
    
    this method tells the cursor to go back to an index of our choice.
    To go back to the beginning of text in the text.txt file, we would 
    use: my_file.seek(0)
    
    This tells the program to read the file content at index 0, the beginning of the content.
    
    We could also use print(my_file.readline()) which tells the program to read one line of text rather than all of the text file.
    
    Once you're done working with the file, you have to close it. This can be done as follows:
        my_file.close()
        
Read, Write, Append

    There are better ways to work with files in Python. For example, to avoid the peskiness of having to close the file manually, we can use
    the following line of code:
        
        with open('test.txt', mode='r') as my_file:
            print(my_file.readlines)
            
    Essentially, this line of code tells the interpreter to open the test.txt file in read mode and refer to it as variable name my_file.
    
    To open the file in read and write mode, we would change mode='r' to mode='r+'
    
    Now how do we write to the file?
    
    We could accomplish this as follows: 
    
    with open('test.txt', mode='r+') as my_file:
        text = my_file.write("hey it's me!")
        print(text)
        
    It is important to note that whenever we write to the file, the cursor resets to index 0, meaning we would be overwriting whatever text is 
    already there. We can append to the text file instead, ensuring that we are not overwriting that which has already been written.
    To do this, we change mode to mode='a'
    
    with open('test.txt', mode='a') as my_file:
        text = my_file.write(":)")
        print(text)
        
    We can also use the write mode which will ignore if the file has content already and completely overwrite the entire file:
    with open('test.txt', mode='w') as my_file:
        * do stuff *
        
File I/O errors
    
    It is good practice to wrap your File I/O statements with a try-except statement:
    
        try:
            with open('sad.txt', mode='r') as my_file:
                print(my_file.read())
        except FileNotFoundError as err:
            print("file does not exist")
            raise err
     
    This will let us know the file does not exist if it cannot be found by our program.
    
    We can also give an error message for I/O errors (such as providing an invalid mode):
    
    try:
            with open('sad.txt', mode='x') as my_file:
                print(my_file.read())
        except FileNotFoundError as err:
            print("file does not exist")
            raise err
        except IOError as err:
            print("I/O error")
            raise err
     
    In this instance, the program would error out and inform you that the program has failed due to an I/O error
