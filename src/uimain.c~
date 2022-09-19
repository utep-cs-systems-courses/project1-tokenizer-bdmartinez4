#include <stdio.h>
#include <stdlib.h>
#include "tokenizer.h"
#include "history.h"
#define BUFFER_SIZE 100

//in case a '!' is seen at user_input[0]
static void process_input(char *user_input, List *history, int history_length) {
  //displays history
  if(user_input[1] == ' ' || user_input[1] == '\0' || user_input[1] == 'h') {
    printf("\t---- HISTORY ----\n");
    print_history(history);
    printf("\t----------------\n");
  }

  else if(user_input[1] == 'q') {
    free_history(history);
    puts("---- EXITING TOKENIZER... ----\n");
    exit(EXIT_SUCCESS);
  }

  else {
    int asked_index = atoi(user_input + 1);
    if(asked_index > 0) {
      char *str = get_history(history, history_length - asked_index + 1);
      if(!str) {
	puts("---- NO HISTORY FOUND AT GIVEN INDEX ----");
	return;
      }
      
      char **tokens = tokenize(str);
      print_tokens(tokens);
      free_tokens(tokens);
    }
    else {
      puts("---- INVALID INDEX ----");
      return;
    }
  }
}

int main() {
  char user_input[BUFFER_SIZE];
  List *history = init_history();
  char **tokens;
  int history_length = 0;
  puts("---------------------");
  puts("Welcome to Tokenizer!");
  puts("---------------------");
  puts("Availiable operations to run:\n\t1. Type a string to store it.\n\t2. Type '!<num>' to print a past entry.\n\t3. Type '!h'|'!' to display all previous entries.\n\t4. Type '!q' to quit Tokenizer\n");
  while(1) {
    printf("> ");
    fgets(user_input, BUFFER_SIZE, stdin);
    //check for '!' commands
    if(user_input[0] == '!') {
      process_input(user_input, history, history_length);
    }
    else {
      add_history(history, user_input);
      puts("String successfully stored!");
      puts(user_input);
      history_length++;
    }
  }
}
