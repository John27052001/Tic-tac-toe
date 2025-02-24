**Tic-Tac-Toe Game with AI using the Minimax algorithm.**

Project Overview:
Game: Tic-Tac-Toe (3x3 grid)
Players: One player vs AI (AI plays optimally)

AI Algorithm: 
Minimax algorithm, which will make the best possible move for AI based on the game state

Technologies:
Python 

1. Define the Game Board
# Tic-Tac-Toe Game Board
board = [' ' for _ in range(9)]  # A list of size 9 to represent the board (empty spaces)
# Mapping positions on the board to indices
# index 0-8 corresponds to positions on a 3x3 grid.
Create a function to print the board:
def print_board(board):
    print("\n")
    for i in range(3):
        print(f" {board[i*3]} | {board[i*3 + 1]} | {board[i*3 + 2]} ")
        if i < 2:
            print("---|---|---")
    print("\n")

2. Check for Win Conditions
Next, we need to create a function to check if a player has won the game

def check_winner(board, player):
    # Check all rows, columns, and diagonals
    win_conditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],  # Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8],  # Columns
        [0, 4, 8], [2, 4, 6]  # Diagonals
    ]
    
    for condition in win_conditions:
        if board[condition[0]] == board[condition[1]] == board[condition[2]] == player:
            return True
    return False

3. Minimax Algorithm for AI
The AI will use the Minimax algorithm to determine the best possible move

def minimax(board, depth, is_maximizing_player):
    # AI plays 'X' and the human player plays 'O'
    if check_winner(board, 'X'):
        return 1  # Maximizing player wins
    elif check_winner(board, 'O'):
        return -1  # Minimizing player wins
    elif ' ' not in board:
        return 0  # Draw, no more moves
    
    if is_maximizing_player:
        best = -float('inf')
        for i in range(9):
            if board[i] == ' ':
                board[i] = 'X'
                best = max(best, minimax(board, depth + 1, False))
                board[i] = ' '  # Undo move
        return best
    else:
        best = float('inf')
        for i in range(9):
            if board[i] == ' ':
                board[i] = 'O'
                best = min(best, minimax(board, depth + 1, True))
                board[i] = ' '  # Undo move
        return best

4. AI Move Function
This function will find the best possible move for the AI

def find_best_move(board):
    best_val = -float('inf')
    best_move = -1
    
    # Try every possible move to find the best one
    for i in range(9):
        if board[i] == ' ':
            board[i] = 'X'  # AI's move
            move_val = minimax(board, 0, False)
            board[i] = ' '  # Undo move
            
            if move_val > best_val:
                best_val = move_val
                best_move = i
    
    return best_move

5. Player's Move
Allow the human player to enter a move and update the board

def player_move(board):
    while True:
        try:
            move = int(input("Enter your move (1-9): ")) - 1
            if board[move] == ' ':
                board[move] = 'O'
                break
            else:
                print("This position is already taken.")
        except (ValueError, IndexError):
            print("Invalid move. Please enter a number between 1 and 9.")
            
6. Main Game Loop
Create the main game loop where the player and AI will take turns until there’s a winner or a draw

def play_game():
    print("Welcome to Tic-Tac-Toe!")
    
    while True:
        print_board(board)
        
        # Player's turn
        player_move(board)
        
        if check_winner(board, 'O'):
            print_board(board)
            print("Player wins!")
            break
        
        if ' ' not in board:
            print_board(board)
            print("It's a draw!")
            break
        
        # AI's turn
        print("AI is making a move...")
        best_move = find_best_move(board)
        board[best_move] = 'X'
        
        if check_winner(board, 'X'):
            print_board(board)
            print("AI wins!")
            break
        
        if ' ' not in board:
            print_board(board)
            print("It's a draw!")
            break

7. Finally, run the game loop
if __name__ == "__main__":
    play_game()





 
