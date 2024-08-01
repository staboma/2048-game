import tkinter as tk
import random

class Game2048:
    def __init__(self, master):
        self.master = master
        self.master.title("2048")
        self.grid_size = 4
        self.board = [[0] * self.grid_size for _ in range(self.grid_size)]
        self.score = 0
        self.colors = {
            0: "#9e948a", 2: "#eee4da", 4: "#ede0c8", 8: "#f2b179",
            16: "#f59563", 32: "#f67c5f", 64: "#f65e3b", 128: "#edcf72",
            256: "#edcc61", 512: "#edc850", 1024: "#edc53f", 2048: "#edc22e"
        }
        self.setup_ui()
        self.add_random_tile()
        self.add_random_tile()
        self.update_ui()

    def setup_ui(self):
        self.frame = tk.Frame(self.master, bg="#bbada0")
        self.frame.grid(padx=(50, 50), pady=(50, 50))  

        self.tiles = []
        for i in range(self.grid_size):
            row = []
            for j in range(self.grid_size):
                tile = tk.Label(self.frame, text="", bg="#9e948a", justify=tk.CENTER, font=("Helvetica", 40, "bold"), width=4, height=2)
                tile.grid(row=i, column=j, padx=7, pady=7)
                row.append(tile)
            self.tiles.append(row)
        
        self.score_label = tk.Label(self.master, text=f"Score: {self.score}", font=("Helvetica", 24, "bold"))
        self.score_label.grid(pady=(20, 0))
        
        self.master.update_idletasks()
        self.center_window()
        self.master.bind("<Key>", self.handle_keypress)

    def center_window(self):
        self.master.update_idletasks()
        width = self.master.winfo_width()
        height = self.master.winfo_height()
        x = (self.master.winfo_screenwidth() // 2) - (width // 2)
        y = (self.master.winfo_screenheight() // 2) - (height // 2)
        self.master.geometry('{}x{}+{}+{}'.format(width, height, x, y))

    def update_ui(self):
        for i in range(self.grid_size):
            for j in range(self.grid_size):
                value = self.board[i][j]
                self.tiles[i][j].config(text=str(value) if value != 0 else "", bg=self.colors[value])
        self.score_label.config(text=f"Score: {self.score}")
        self.master.update_idletasks()

    def add_random_tile(self):
        empty_tiles = [(i, j) for i in range(self.grid_size) for j in range(self.grid_size) if self.board[i][j] == 0]
        if empty_tiles:
            i, j = random.choice(empty_tiles)
            self.board[i][j] = random.choice([2, 4])

    def compress(self, row):
        new_row = [i for i in row if i != 0]
        new_row += [0] * (self.grid_size - len(new_row))
        return new_row

    def merge(self, row):
        for i in range(self.grid_size - 1):
            if row[i] == row[i + 1] and row[i] != 0:
                row[i] *= 2
                row[i + 1] = 0
                self.score += row[i]
        return row

    def move_left(self):
        changed = False
        for i in range(self.grid_size):
            compressed = self.compress(self.board[i])
            merged = self.merge(compressed)
            new_row = self.compress(merged)
            if self.board[i] != new_row:
                changed = True
            self.board[i] = new_row
        return changed

    def move_right(self):
        self.reverse_board()
        changed = self.move_left()
        self.reverse_board()
        return changed

    def move_up(self):
        self.transpose_board()
        changed = self.move_left()
        self.transpose_board()
        return changed

    def move_down(self):
        self.transpose_board()
        changed = self.move_right()
        self.transpose_board()
        return changed

    def reverse_board(self):
        for i in range(self.grid_size):
            self.board[i] = self.board[i][::-1]

    def transpose_board(self):
        self.board = [list(row) for row in zip(*self.board)]

    def can_move(self):
        for i in range(self.grid_size):
            for j in range(self.grid_size):
                if self.board[i][j] == 0:
                    return True
                if i < self.grid_size - 1 and self.board[i][j] == self.board[i + 1][j]:
                    return True
                if j < self.grid_size - 1 and self.board[i][j] == self.board[i][j + 1]:
                    return True
        return False

    def handle_keypress(self, event):
        if self.game_over():
            return
        moves = {
            'w': self.move_up,
            'a': self.move_left,
            's': self.move_down,
            'd': self.move_right,
            'Up': self.move_up,
            'Left': self.move_left,
            'Down': self.move_down,
            'Right': self.move_right
        }
        move = moves.get(event.keysym.lower())
        if move and move():
            self.add_random_tile()
            self.update_ui()
            if not self.can_move():
                self.show_game_over()

    def game_over(self):
        if not self.can_move():
            return True
        return False

    def show_game_over(self):
        game_over_frame = tk.Frame(self.master, borderwidth=2)
        game_over_frame.place(relx=0.5, rely=0.5, anchor="center")
        tk.Label(game_over_frame, text="Game Over", font=("Helvetica", 48, "bold"), fg="white", bg="red").pack()

if __name__ == "__main__":
    root = tk.Tk()
    game = Game2048(root)
    root.mainloop()