# tictactoe-game
def print_board(board):
    # Clear the console before printing the board
    print("\033[H\033[J")
    print(" {} | {} | {}".format(board[0], board[1], board[2]))
    print("---|---|---")
    print(" {} | {} | {}".format(board[3], board[4], board[5]))
    print("---|---|---")
    print(" {} | {} | {}".format(board[6], board[7], board[8]))

def get_move(player):
    valid_move = False
    while not valid_move:
        move = input("Player {}, enter your move (1-9): ".format(player))
        try:
            move = int(move) - 1
            if move >= 0 and move <= 8:
                valid_move = True
            else:
                print("Invalid move. Please enter a number between 1 and 9.")
        except ValueError:
            print("Invalid move. Please enter a number between 1 and 9.")
    return move

def check_win(board):
    for i in range(0, 9, 3):
        if board[i] == board[i+1] == board[i+2] and board[i] != " ":
            return board[i]
    for i in range(3):
        if board[i] == board[i+3] == board[i+6] and board[i] != " ":
            return board[i]
    if board[0] == board[4] == board[8] and board[0] != " ":
        return board[0]
    if board[2] == board[4] == board[6] and board[2] != " ":
        return board[2]
    return None

def play_game():
    board = [" "] * 9
    players = ["X", "O"]
    current_player = 0
    winner=0

    while not winner and " " in board:
        print_board(board)
        move = get_move(players[current_player])
        if board[move] == " ":
            board[move] = players[current_player]
            current_player = (current_player + 1) % 2
            winner = check_win(board)
        else:
            print("That space is already taken. Please choose another move.")
    print_board(board)
    if winner:
        print("Player {} wins!".format(winner))
    else:
        print("Tie game.")

play_game()
