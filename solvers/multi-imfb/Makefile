# Makefile for SVDFeature customization

# !!specify HOME PATH
PRJ=../..
export CC  = gcc
export CXX = g++
export CFLAGS = -Wall -O3 -msse2 

# !! change the name of customized code
BIN = svdf_mimfb svdf_mimfb_infer 
OBJ = apex_svd.o apex_svd_data.o
.PHONY: clean all

all: $(BIN)
export LDFLAGS= -pthread -lm 

# !! use apex_svd_mimfb.cpp for customized solver
apex_svd.o:apex_multi_imfb.cpp apex_multi_imfb.h $(PRJ)/apex_svd.h $(PRJ)/apex_svd_model.h $(PRJ)/apex_svd_data.h 
# !! reuse input component of SVDFeature
apex_svd_data.o:$(PRJ)/apex_svd_data.cpp $(PRJ)/apex_svd_data.h

svdf_mimfb:$(PRJ)/svd_feature.cpp apex_svd.o apex_svd_data.o $(PRJ)/apex_svd_data.h $(PRJ)/apex_svd.h 
svdf_mimfb_infer:$(PRJ)/svd_feature_infer.cpp apex_svd.o apex_svd_data.o $(PRJ)/apex_svd_data.h $(PRJ)/apex_svd.h 

$(BIN) : 
	$(CXX) $(CFLAGS) $(LDFLAGS) -o $@ $(filter %.cpp %.o %.c, $^)

$(OBJ) : 
	$(CXX) -c $(CFLAGS) -o $@ $(filter %.cpp %.c, $^)

clean:
	$(RM) $(OBJ) $(BIN) *~

