CC=clang
CPP=clang++
CFLAGS=-ldeepstate_LF -fprofile-instr-generate -fcoverage-mapping -fsanitize=fuzzer,address #-lutf8
CFLAGS_DS=-ldeepstate -fprofile-instr-generate -fcoverage-mapping   #-lutf8
CPPFLAGS=$(CFLAGS) -g #-lutf8 -g
CPPFLAGS_DS=-ldeepstate -fprofile-instr-generate -fcoverage-mapping -g #-lutf8 -g
CPPFLAGS_AFL=-ldeepstate_AFL -fprofile-instr-generate -fcoverage-mapping
LINKER_OPTS=-L${CURDIR}/libutf8/

all: main main_lf main_afl
.PHONY: all

main_lf: Test.cpp libutf8/encode.o libutf8/decode.o
	$(CPP) $(LINKER_OPTS) $^ $(CPPFLAGS) -o $@

main: Test.cpp libutf8/encode.o libutf8/decode.o
	$(CPP) $(LINKER_OPTS) $^ $(CPPFLAGS_DS) -o $@

main_afl: Test.cpp libutf8/encode.o libutf8/decode.o
	afl-clang++ $(LINKER_OPTS) $^ $(CPPFLAGS_AFL) -o $@

clean:
	rm main main_afl main_lf
