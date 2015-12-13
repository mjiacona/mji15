# mji15
NONE = '.'
P1 = 'X'
P2 = 'O'
        
class Game:
    def __init__ (self, cols = 6, rows = 7, ToWin = 4):
        """Create a new game."""
        self.cols = cols
        self.rows = rows
        self.win = ToWin
        self.board = [[NONE] * rows for _ in range(cols)]

    def insert (self, column, player):
        """Insert piece in given column."""
        col = self.board[column]
        if col[0] != NONE:
            raise Exception('Column full')
        i = -1
        while col[i] != NONE:
            i -= 1
        col[i] = player
        self.checkWin()

        
    def checkWin (self):
        """Check  for a winner."""
        w = self.getWin()
        if w:
            self.printBoard()
            raise Exception(w + ' won!')

            
    def getWin(board, position):
        """finds winner on board"""
        self.boardHeight = 6
        selfboardWidth = 7

        #horizontal 
        for y in range(boardHeight):
            for x in range(boardWidth - 3):
                if board[row][col] == position and board[row+1][col] == position and board[row+2][col] == position and board[row+3][col] == position:
                    return True

        # vertical 
        for x in range(boardWidth):
            for y in range(boardHeight - 3):
                if board[x][y] == position and board[x][y+1] == position and board[x][y+2] == position and board[x][y+3] == position:
                    return True
        
        # \ diagonal 
        for x in range(boardWidth - 3):
            for y in range(boardHeight - 3):
                if board[x][y] == position and board[x+1][y+1] == position and board[x+2][y+2] == position and board[x+3][y+3] == position:
                    return True

        #  / diagonal 
        for x in range(boardWidth - 3):
            for y in range(3, boardHeight):
                if board[x][y] == position and board[x+1][y-1] == position and board[x+2][y-2] == position and board[x+3][y-3] == position:
                    return True

        return False



    def printBoard (self):
        """Print  board"""
        print('  '.join(map(str, range(self.cols))))
        for y in range(self.rows):
            print('  '.join(str(self.board[x][y]) for x in range(self.cols)))
        print()

def diagonalN (M, cols, rows):
    """Get negative diagonals"""
    for diagonal in ([(j, i - cols + j + 1) for j in range(cols)] for i in range(cols + rows - 1)):
        yield [M[i][j] for i, j in di if i >= 0 and j >= 0 and i < cols and j < rows]


def diagonalP (M, cols, rows):
    """Get positive diagonals"""
    for diagonal in ([(j, i - j) for j in range(cols)] for i in range(cols + rows -1)):
        yield [M[i][j] for i, j in di if i >= 0 and j >= 0 and i < cols and j < rows]


if __name__ == '__main__':
    g = Game()
    turn = P1
    while True:
        g.printBoard()
        row = input('{}\'s turn: '.format('P1' if turn == P1 else 'P2'))
        g.insert(int(row), turn)
        turn = P2 if turn == P1 else P1

