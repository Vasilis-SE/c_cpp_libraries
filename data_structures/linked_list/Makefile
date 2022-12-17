CC = g++
CFLAGS = -g -Wall

# Naming
SRC = src
INCLUDES = includes
HEADERS = headers
IMPLEMENTATIONS = templates
BINARY_DIR = bin
BINARY = linked_list
OBJ_DIR = build
LIB_DIR = lib

# Path variables
HOME = $(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))

SRC_PATH = $(HOME)/$(SRC)
SRC_INC_PATH = $(SRC_PATH)/$(INCLUDES)
SRC_H_PATH = $(SRC_INC_PATH)/$(HEADERS)
SRC_I_PATH = $(SRC_INC_PATH)/$(IMPLEMENTATIONS)

OBJ_PATH = $(HOME)/$(OBJ_DIR)
OBJ_INC_PATH = $(OBJ_PATH)/$(INCLUDES)
OBJ_H_PATH = $(OBJ_INC_PATH)/$(HEADERS)
OBJ_I_PATH = $(OBJ_INC_PATH)/$(IMPLEMENTATIONS)

BINARY_PATH = $(HOME)/$(BINARY_DIR)

# Files variables
SRC_FILES = $(wildcard $(SRC_PATH)/*.cpp)
SRC_H_FILES = $(wildcard $(SRC_H_PATH)/*.hpp)
SRC_I_FILES = $(wildcard $(SRC_I_PATH)/*.ipp)

OBJ_FILES= $(subst src,build, $(patsubst %.cpp, %.o, $(SRC_FILES)))    
OBJ_H_FILES= $(subst src,build, $(patsubst %.hpp, %.o, $(SRC_H_FILES)))    
OBJ_I_FILES= $(subst src,build, $(patsubst %.ipp, %.o, $(SRC_I_FILES)))    

OUTPUT = $(BINARY_PATH)/$(BINARY).exe

# ------- Rules ---------

# Build object file(-s) for src folder 
$(OBJ_FILES): $(SRC_FILES)
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -c $< -o $@ 

# Build object file(-s) for headers folder
$(OBJ_H_FILES): $(SRC_H_FILES)
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -c $< -o $@

# Build object file(-s) for templates folder
$(OBJ_I_FILES): $(SRC_I_FILES)
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -x c++ -c $< -o $@ 

build_objects: $(OBJ_H_FILES) $(OBJ_I_FILES) $(OBJ_FILES)
# $(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -c $(SRC_PATH)/main.cpp -o $(OBJ_PATH)/main.o

build_exe: 
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -g $(SRC_PATH)/main.cpp -o $(OUTPUT)

# Create necessary folders for build purpose
foldering: 
	mkdir $(BINARY_DIR)
	mkdir $(OBJ_DIR)
	mkdir $(OBJ_DIR)/$(INCLUDES)
	mkdir $(OBJ_DIR)/$(INCLUDES)/$(HEADERS)
	mkdir $(OBJ_DIR)/$(INCLUDES)/$(IMPLEMENTATIONS)

# Clean old folders and files for build purpose
clean:
	rm -rf $(OBJ_DIR)/
	rm -rf $(BINARY_DIR)/
	
all: clean foldering build_objects

