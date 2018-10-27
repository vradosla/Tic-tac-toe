# Tic-tac-toe
Tic-tac-toe in python

# Order of playing

import random

def choose_first():
    go_first=random.randint(1,10)
    if go_first <= 5:
        print("Player 1 goes first")
        return "Player 1"
    else:
        print("Player 2 goes first")
        return "Player 2"

# Player input

def player_input(on_turn_player):
    if on_turn_player == "Player 1":
        print(" Player 1, please select 'X' or 'O'")
    else:
        print(" Player 2, please select 'X' or 'O'")
        
    from IPython.display import clear_output
    
    Player1 =""
    Player2 =""

    
    while Player1 != "X" and Player2 !="X" and Player1 !="O" and Player2 !="O":
        if on_turn_player == "Player 1":
            Player1= input()
            print(f" {on_turn_player}, please select 'X' or 'O'")
        elif on_turn_player == "Player 2":
            Player2= input()
            print(f" {on_turn_player}, please select 'X' or 'O'")
    else:
        if on_turn_player == "Player 1" and Player1 == "X":
            clear_output()
            Player2 = "O"
            print(f"Player 1 gets '{Player1}' and Player 2 gets '{Player2}'")
            return Player1
        elif on_turn_player == "Player 1" and Player1 == "O":
            clear_output()
            Player2 = "X"
            print(f"Player 1 gets '{Player1}' and Player 2 gets '{Player2}'")
            return Player1
        elif on_turn_player == "Player 2" and Player2 == "X":
            clear_output()
            Player1 = "O"
            print(f"Player 1 gets '{Player1}' and Player 2 gets '{Player2}'")
            return Player2
        elif on_turn_player == "Player 2" and Player2 == "O":
            clear_output()
            Player1 = "X"
            print(f"Player 1 gets '{Player1}' and Player 2 gets '{Player2}'")
            return Player2
            


# Board 

from IPython.display import clear_output
clear_output()

def display_board(board):
    
    print("   |   |   ")
    print(f" {board[1]}   {board[2]}   {board[3]} ")
    print("   |   |   ")
    print(f"___________")
    print("   |   |   ")
    print(f" {board[4]}   {board[5]}   {board[6]} ")
    print("   |   |   ")
    print(f"____________")
    print("   |   |   ")
    print(f" {board[7]}   {board[8]}   {board[9]} ")
    print("   |   |   ")
    print(f"          ")
    
# Win check

def win_check(board, mark):

    #Horizontal check:
    if (board[1] == board[2] == board[3] == marker) or (board[4] == board[5] == board[6] == marker) or (board[7] == board[8] == board[9] == marker):
        return True
    
    #Vertical check:
    elif (board[1] == board[4] == board[7] == marker) or (board[2] == board[5] == board[8] == marker) or (board[3] == board[6] == board[9] == marker):
        return True
    
    #Diagonal check:
    elif (board[1] == board[5] == board[9] == marker) or (board[3] == board[5] == board[7] == marker):
        return True
    
    else:
        return False
    
# Space availability check

def space_check(board, position):
    return board[position] == ""

# Player moves

def player_choice(board):
    next_move = input(f"{on_turn_player} ('{marker}') please select your next move (1-9): ")
    while next_move not in ["1","2","3","4","5","6","7","8","9"]:
        next_move = input("Please select a valid next move (1-9): ")
    else:
        next_move = int(next_move)
    
    while space_check(board,next_move) != True:
        next_move = input("Please select a valid next move (1-9): ")
        while next_move not in ["1","2","3","4","5","6","7","8","9"]:
            next_move = input("Please select a valid next move : ")
        else:
            next_move = int(next_move)  
    else:    
        return int(next_move)
    
# Write on board

def place_marker(board, marker, position):
    starting_board[int(position)] = marker
    
# Check full board

def full_board_check(board):
    return board[1] != "" and board[2] !=  ""  and board[3] !=  "" and board[4] !=  "" and board[5] !=  "" and board[6] !=  "" and board[7] !=  "" and board[8] !=  "" and board[9] !=  ""

# Replay

def replay():
    play_again= str(input("Do you want to play again? Please type yes or no. "))
    while play_again != "yes":
        if play_again == "no":
            print("Thanks for playing")
            return play_again == "yes"
        else:
            play_again= str(input("Do you want to play again? - please type 'yes' or 'no'. "))
    else:
        return play_again == "yes"
        
 # The game setup:
 
 def game():
    print('Welcome to Tic Tac Toe!')

    import random
    from IPython.display import clear_output
    global on_turn_player
    on_turn_player = choose_first()
    global marker
    marker = player_input(on_turn_player)
    
    global starting_board
    starting_board = ['#','','','','','','','','','']
    display_board(starting_board)

    chosen_position = player_choice(starting_board)
    place_marker(starting_board, marker, chosen_position)
    clear_output()
    display_board(starting_board)

    while not win_check(starting_board,marker):
        if full_board_check(starting_board):
            print("Draw!")
            replay()
            break
        elif marker == "X" and on_turn_player == "Player 1":
            marker = "O"
            on_turn_player = "Player 2"
            chosen_position = player_choice(starting_board)
            place_marker(starting_board, marker, chosen_position)
            clear_output()
            display_board(starting_board)
        elif marker == "X" and on_turn_player == "Player 2":
            marker = "O"
            on_turn_player = "Player 1"
            chosen_position = player_choice(starting_board)
            place_marker(starting_board, marker, chosen_position)
            clear_output()
            display_board(starting_board)
        elif marker == "O" and on_turn_player == "Player 1":
            marker = "X"
            on_turn_player = "Player 2"
            chosen_position = player_choice(starting_board)
            place_marker(starting_board, marker, chosen_position)
            clear_output()
            display_board(starting_board)
        elif marker == "O" and on_turn_player == "Player 2":
            marker = "X"
            on_turn_player = "Player 1"
            chosen_position = player_choice(starting_board)
            place_marker(starting_board, marker, chosen_position)
            clear_output()
            display_board(starting_board)
    else:
        print(f"{on_turn_player} you win!!!")
        replay()
        
 # Final Function and replay:
 
 def tic_tac_toe():
    global if_replay
    if_replay = game()
    while if_replay:
        game()
        global if_replay
        if_replay = game()
    else:
        global if_replay
        if_replay = False
