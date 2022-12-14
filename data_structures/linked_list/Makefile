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
TEST_DIR = test

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

TEST_PATH = $(HOME)/$(TEST_DIR)
BINARY_PATH = $(HOME)/$(BINARY_DIR)
LIBRARY_PATH = $(HOME)/$(LIB_DIR)

# Files variables
SRC_FILES = $(wildcard $(SRC_PATH)/*.cpp)
SRC_H_FILES = $(wildcard $(SRC_H_PATH)/*.hpp)
SRC_I_FILES = $(wildcard $(SRC_I_PATH)/*.ipp)

OBJ_FILES= $(subst src,build, $(patsubst %.cpp, %.o, $(SRC_FILES)))    
OBJ_H_FILES= $(subst src,build, $(patsubst %.hpp, %.o, $(SRC_H_FILES)))    
OBJ_I_FILES= $(subst src,build, $(patsubst %.ipp, %.o, $(SRC_I_FILES)))  

LIB_HOME = D:/repositories/c_cpp_libraries/data_structures/linked_list/lib/linux

OUTPUT = $(BINARY_PATH)/$(BINARY).exe

# Build object file(-s) for src folder 
$(OBJ_FILES): $(SRC_FILES)
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -c $< -o $@ 

# Build object file(-s) for headers folder
$(OBJ_H_FILES): $(SRC_H_FILES)
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -c $< -o $@

# Build object file(-s) for templates folder
$(OBJ_I_FILES): $(SRC_I_FILES)
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -x c++ -c $< -o $@ 

compile_source: $(OBJ_H_FILES) $(OBJ_I_FILES) $(OBJ_FILES)
# $(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -c $(SRC_PATH)/main.cpp -o $(OBJ_PATH)/app.o

generate_executable: 
	$(CC) -I $(SRC_H_PATH) -I $(SRC_I_PATH) -g $(SRC_PATH)/main.cpp -o $(OUTPUT)

lib_sll_linux: 
	$(CC) -shared -fpic -o $(LIBRARY_PATH)/linux/libsll.so \
		$(OBJ_I_PATH)/node.o \
		$(OBJ_I_PATH)/linked_list.o \
		$(OBJ_I_PATH)/singly_linked_list.o 

lib_sll_windows: 
	$(CC) -shared -o $(LIBRARY_PATH)/windows/libsll.dll \
		$(OBJ_I_PATH)/node.o \
		$(OBJ_I_PATH)/linked_list.o \
		$(OBJ_I_PATH)/singly_linked_list.o 

# Create necessary folders for build purpose
objects_foldering: 
	mkdir $(OBJ_DIR)
	mkdir $(OBJ_DIR)/$(INCLUDES)
	mkdir $(OBJ_DIR)/$(INCLUDES)/$(HEADERS)
	mkdir $(OBJ_DIR)/$(INCLUDES)/$(IMPLEMENTATIONS)

binaries_foldering:
	mkdir $(BINARY_DIR)

libraries_foldering: 
	mkdir $(LIB_DIR)
	mkdir $(LIB_DIR)/linux
	mkdir $(LIB_DIR)/windows

# Clean old folders and files for build purpose
objects_clean:
	rm -rf $(OBJ_DIR)/

binaries_clean: 
	rm -rf $(BINARY_DIR)/

libraries_clean: 
	rm -rf $(LIB_DIR)/

# Processes that utilize that above targets.
compile: objects_clean objects_foldering compile_source

liblin: libraries_clean libraries_foldering lib_sll_linux

libwin: libraries_clean libraries_foldering lib_sll_windows

test_env: 
	$(CC) -c $(TEST_PATH)/main.cpp -o $(TEST_PATH)/main.o
	$(CC) -o $(TEST_PATH)/main $(TEST_PATH)/main.o -l :libsll.so -L$(LIB_HOME)
# $(CC) -o $(TEST_PATH)/main $(TEST_PATH)/main.o -l :libsll.so -L$(LIB_HOME) -Wl,-rpath,$(LIB_HOME)