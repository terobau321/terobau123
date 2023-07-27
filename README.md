# terobau123
tic tac toe
def print_board(board):
    for row in board:
        print("|".join(row))
        print("-----")


def check_win(board, player):
    for row in board:
        if all(cell == player for cell in row):
            return True

    for col in range(3):
        if all(board[row][col] == player for row in range(3)):
            return True

    if all(board[i][i] == player for i in range(3)) or all(board[i][2 - i] == player for i in range(3)):
        return True

    return False


def check_draw(board):
    return all(board[row][col] != " " for row in range(3) for col in range(3))


def get_move(player):
    while True:
        move = input(f"Player {player}, enter your move (row[1-3] col[1-3]): ")
        try:
            row, col = map(int, move.split())
            if 1 <= row <= 3 and 1 <= col <= 3:
                return row - 1, col - 1
            else:
                print("Invalid input! Row and column must be between 1 and 3.")
        except ValueError:
            print("Invalid input! Please enter row and column numbers separated by a space.")


def play_tic_tac_toe():
    board = [[" " for _ in range(3)] for _ in range(3)]
    players = ["X", "O"]
    player_idx = 0

    while True:
        print_board(board)

        player = players[player_idx]
        row, col = get_move(player)

        if board[row][col] == " ":
            board[row][col] = player
            if check_win(board, player):
                print_board(board)
                print(f"Player {player} wins!")
                break
            elif check_draw(board):
                print_board(board)
                print("It's a draw!")
                break

            player_idx = (player_idx + 1) % 2
        else:
            print("Cell already taken. Try again.")

if __name__ == "__main__":
    play_tic_tac_toe()
