#ID:206751976
#Email:"aharonba123@gmail.com"

#!make -f
#valgrind ./demo

CXX=clang++
CXXFLAGS=-std=c++11 -Werror -Wsign-conversion
VALGRIND_FLAGS=-v --leak-check=full --show-leak-kinds=all  --error-exitcode=99

SOURCES=Player.cpp Resource.cpp Demo.cpp Vertex.cpp Edge.cpp Tile.cpp Board.cpp Catan.cpp Card.cpp
SOURCES_WITHOUT_DEMO=Player.cpp Resource.cpp Vertex.cpp Edge.cpp Tile.cpp Board.cpp Catan.cpp Card.cpp

OBJECTS=$(subst .cpp,.o,$(SOURCES))
OBJECTS2=$(subst .cpp,.o,$(SOURCES_WITHOUT_DEMO))


catan: demo
	./$^

demo: Demo.o $(OBJECTS)
	$(CXX) $(CXXFLAGS) $^ -o demo

%.o: %.cpp
	$(CXX) $(CXXFLAGS) -c $< -o $@

test: Test.o $(OBJECTS2)
	$(CXX) $(CXXFLAGS) $^ -o test

# tidy:
# 	clang-tidy $(SOURCES) -checks=bugprone-*,cppcoreguidelines-*,performance-*,portability-*,readability-*,clang-analyzer-*,-cppcoreguidelines-pro-bounds-pointer-arithmetic,-cppcoreguidelines-owning-memory --warnings-as-errors=-* --

valgrind: demo 
	valgrind --tool=memcheck $(VALGRIND_FLAGS) ./demo 2>&1 | { egrep "lost| at " || true; }

# %.o: %.cpp
# 	$(CXX) $(CXXFLAGS) --compile $< -o $@

clean:
	rm -f *.o demo test json