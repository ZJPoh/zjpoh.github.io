---
title: 'Hello Makefile'
date: 2018-07-30
permalink: /posts/2018/07/hello-world
tags:
  - cs
excerpt: 'Sample C++ project with makefile'
---

I mainly used C++ in my research but I never had to setup a C++ project.
So, I actually don't know how to setup a C++ project with Makefile.
In this post, I will outline the steps of a basic C++ repo.

## Structure of the Repo

* `bin/`: Directory for compiled binary
* `data/`: Directory containing data files
* `doc/`: Directory containing documentation
* `include/`: Directory for header files
* `lib/`: Directory containing static library files
* `obj/`: Directory containing object files
* `src/`: Directory containing source `.cpp` code
* Makefile
* README.md

## Makefile

Makefile with comments

```make
CC = g++ # Compiler

TARGET = bin/hellomake # Compiled binary file

SRC_DIR = src
OBJ_DIR = obj
INC_DIR = include
LIB_DIR = lib

SRC_EXT = cpp # File extension of c++
CPPFLAGS = -std=gnu++11 -Wall # Specify C++ Flages
                            # Use C++11 and print all warning
LIB = -pthread -L$(LIB_DIR) # Specify library to include
                            # -pthread for multi-threading
                            # Note: $(VAR) return variable value
INC = -I$(INC_DIR) # Include in compilation

SRC_FILES = $(shell find $(SRC_DIR) -type f -name *.$(SRC_EXT))
    # Find all source files with file extension $(SRC_EXT)
OBJ_FILES = $(patsubst $(SRC_DIR)/%.$(SRC_EXT),$(OBJ_DIR)/%.o,$(SRC_FILES))
    # Get the list of source files from $(SRC_FILES),
    # replace .$(SRC_EXT) with .o and set them as a list of object files

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.$(SRC_EXT)
	$(CC) $(CPPFLAGS) $(LIB) $(INC) -c -o $@ $<
    # Compile all the object files to object directory using source files
    # The second line is basically what you would run in CLI
    # to compile the object fies
    # %@ is everything before :
    # $< is the first item after :
    # Note: Have to use tab.

$(TARGET): $(OBJ_FILES)
	$(CC) $(CPPFLAGS) $(LIB) $(INC) -o $@ $^
    # Compile binary file using the object files
    # $^ is everythign after :

.PHONY: clean  # Ignore filename called clean when runing make clean

clean:  # Clean up generated files so that one can make from scratch
	$(RM) -r $(OBJ_DIR) $(TARGET)  # Remove object directory and target
	mkdir -p $(OBJ_DIR)  # Recreate object directory
```

## Reference

My [hello makefile repo](https://github.com/zjpoh/hello_makefile).
