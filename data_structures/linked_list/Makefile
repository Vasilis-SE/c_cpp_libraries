CC = g++

# Naming
SRC = src
INCLUDES = includes
HEADERS = headers
IMPLEMENTATIONS = templates
BINARY_DIR = bin
BINARY = linked_list
OBJ_DIR = build

# Path variables
HOME = $(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))
SRC_PATH = $(HOME)/$(SRC)
INC_PATH = -I$($(SRC_PATH)/$(INCLUDES))
H_PATH = -I$($(INC_PATH)/$(HEADERS))
I_PATH = -I$($(INC_PATH)/$(IMPLEMENTATIONS))
OBJ_PATH = $(HOME)/$(OBJ_DIR)
BINARY_PATH = $(HOME)/$(BINARY_DIR)

# Files variables
SRC_FILES = $(wildcard $(SRC_PATH)/*.cpp)
H_FILES = $(wildcard $(H_PATH)/*.hpp)
I_FILES = $(wildcard $(I_PATH)/*.ipp)
OBJ_FILES = $(patsubst $(SRC_PATH)/%.cpp, $(OBJ_PATH)/%.o, $(SRC_FILES))

OUTPUT = $(BINARY_PATH)/$(BINARY).exe

#Makefile rules
$(OBJ_PATH)/%.o: $(SRC_PATH)/%.cpp
	$(CC) $(OBJ_PATH) -c -o $@ $<

$(OBJ_PATH)/$(INCLUDES)/$(IMPLEMENTATIONS)/%.o: $(OBJ_PATH)/$(INCLUDES)/$(HEADERS)/%.o
	$(CC) $(I_PATH) -c -o $@ $<

$(OBJ_PATH)/$(INCLUDES)/$(HEADERS)/%.o:
	$(CC) $(H_PATH) -c -o $@ $<

$(OUTPUT): $(OBJ_FILES) Makefile
	$(CC) $(OBJ_FILES) -o $(OUTPUT)

# Makefile commands
clean:
	rm -rf $(OBJ_DIR)/
	rm -rf $(BINARY_DIR)/
	
build:
	mkdir $(BINARY_DIR)
	mkdir $(OBJ_DIR)
	mkdir $(OBJ_DIR)/$(INCLUDES)
	mkdir $(OBJ_DIR)/$(INCLUDES)/$(HEADERS)
	mkdir $(OBJ_DIR)/$(INCLUDES)/$(IMPLEMENTATIONS)

	$(OBJ_PATH)/%.o
