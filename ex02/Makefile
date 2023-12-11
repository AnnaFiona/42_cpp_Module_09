NAME = PmergeMe

CXX = c++
CXXFLAGS = -g -Wall -Werror -Wextra -std=c++98

SRC =	main.cpp PmergeMe.cpp
T_SRC = tests.cpp PmergeMe.cpp

DEP =	PmergeMe.hpp

OBJDIR = ./objects_and_dependencies/
OBJFILES = $(SRC:.cpp=.o)
OBJ = $(addprefix $(OBJDIR), $(OBJFILES))

T_OBJFILES = $(T_SRC:.cpp=.o)
T_OBJ = $(addprefix $(OBJDIR), $(T_OBJFILES))

.PHONY: clean fclean all re run val

all: $(NAME)

$(OBJDIR)%.o: ./%.cpp $(DEP)
	$(CXX) $(CXXFLAGS) -MMD -MP $< -o $@ -c

$(OBJDIR):
	mkdir -p $(OBJDIR)

$(NAME): $(OBJDIR) $(OBJ)
	$(CXX) $(CXXFLAGS) $(OBJ) -o $(NAME)

tests: $(OBJDIR) $(T_OBJ)
	$(CXX) $(CXXFLAGS) $(T_OBJ) -o tests
	valgrind ./tests

clean:
	@rm -rf $(OBJDIR)
	@echo all .o and .d files deleted

fclean: clean
	@rm -f $(NAME) tests
	@echo
	@echo ...and the executable too

re: fclean all

run: $(NAME)
	./$(NAME)

val: $(NAME)
	valgrind ./$(NAME)