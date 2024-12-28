# x-and-o

def print_board(board):
    print(f"\n {board[0]} | {board[1]} | {board[2]} ")
    print("-----------")
    print(f" {board[3]} | {board[4]} | {board[5]} ")
    print("-----------")
    print(f" {board[6]} | {board[7]} | {board[8]} \n")

# Function to check if the current player has won
def check_win(board, player):
    win_conditions = [
        [0, 1, 2],  # Top row
        [3, 4, 5],  # Middle row
        [6, 7, 8],  # Bottom row
        [0, 3, 6],  # Left column
        [1, 4, 7],  # Middle column
        [2, 5, 8],  # Right column
        [0, 4, 8],  # Diagonal 1
        [2, 4, 6],  # Diagonal 2
    ]
    
    for condition in win_conditions:
        if all(board[i] == player for i in condition):
            return True
    return False

# Function to check if the board is full (draw situation)
def is_board_full(board):
    return " " not in board

# Main function to run the game
def play_game():
    # Initial game board (3x3 grid)
    board = [" "] * 9
    current_player = "X"  # X starts first
    
    print("Welcome to Tic-Tac-Toe!")
    
    while True:
        # Print the current board
        print_board(board)
        
        # Get the player's move
        try:
            move = int(input(f"Player {current_player}, enter your move (1-9): ")) - 1
        except ValueError:
            print("Invalid input! Please enter a number between 1 and 9.")
            continue
        
        # Validate move
        if move < 0 or move > 8 or board[move] != " ":
            print("Invalid move! That position is already taken or out of range.")
            continue
        
        # Update the board with the current player's move
        board[move] = current_player
        
        # Check if the current player has won
        if check_win(board, current_player):
            print_board(board)
            print(f"Player {current_player} wins!")
            break
        
        # Check for a draw
        if is_board_full(board):
            print_board(board)
            print("It's a draw!")
            break
        
        # Switch to the other player
        current_player = "O" if current_player == "X" else "X"

# Start the game
if __name__ == "__main__":
    play_game()
