SRCS    = main.cpp Animal.cpp Cat.cpp Dog.cpp WrongAnimal.cpp WrongCat.cpp
HEADERS =          Animal.hpp Cat.hpp Dog.hpp WrongAnimal.hpp WrongCat.hpp
OBJS    = $(SRCS:.cpp=.o)
OBJS   := $(addprefix ./objs/, $(OBJS))
FLAGS   = -std=c++98 -Wall -Wextra -Werror
CPP     = c++

all: $(OBJS) $(HEADER)
	clear
	$(CPP) $(FLAGS) $(SRCS)

./objs/%.o: %.cpp
	mkdir ./objs/ 2> /dev/null || true
	$(CPP) -o $@ -c $<

clean:
	rm -f $(OBJS)
	rmdir ./objs/ 2> /dev/null || true

fclean: clean
	rm -f a.out

re: fclean all

.PHONY: all, clean, fclean, re, debug
