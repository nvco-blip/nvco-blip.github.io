# # Créé par nicol, le 22/11/2020 en Python 3.7

from tkinter import *

def drawLines():
    can.create_line(0,100, 300, 100)
    can.create_line(0,200, 300, 200)
    can.create_line(100, 0, 100, 300)
    can.create_line(200, 0, 200, 300)

def printGrid():
    print(grid[0])
    print(grid[1])
    print(grid[2])
    print(" ")

def pointeur(event):
    global player, grid
    x = event.x
    y = event.y
    if x < 100:
        column = 0
    elif x < 200:
        column = 1
    else :
        column = 2

    if y < 100:
        line = 0
    elif y < 200:
        line = 1
    else :
        line = 2

    if winner == 0:
        if player == True and grid[line][column] == 0:
            grid[line][column] = 1
            drawCircle(column, line)
            player = False
        elif player == False and grid[line][column] == 0:
            grid[line][column] = 2
            drawCircle(column, line)
            player = True

    printGrid()
    verifWin()

def drawCircle(col, line):
    if player == True:
        if col == 0 :
            if line == 0:
                can.create_oval(10,10,90,90, outline="blue")
            elif line == 1:
                can.create_oval(10, 110, 90, 190, outline="blue")
            else :
                can.create_oval(10,210, 90, 290, outline="blue")
        if col == 1:
            if line == 0:
                can.create_oval(110,10,190,90, outline="blue")
            elif line == 1:
                can.create_oval(110, 110, 190, 190, outline="blue")
            else :
                can.create_oval(110,210, 190, 290, outline="blue")
        elif col == 2 :
            if line == 0:
                can.create_oval(210,10,290,90, outline="blue")
            elif line == 1:
                can.create_oval(210, 110, 290, 190, outline="blue")
            else :
                can.create_oval(210,210, 290, 290, outline="blue")

    if player == False:
        if col == 0 :
            if line == 0:
                can.create_oval(10,10,90,90, outline="red")
            elif line == 1:
                can.create_oval(10, 110, 90, 190, outline="red")
            else :
                can.create_oval(10,210, 90, 290, outline="red")
        if col == 1:
            if line == 0:
                can.create_oval(110,10,190,90, outline="red")
            elif line == 1:
                can.create_oval(110, 110, 190, 190, outline="red")
            else :
                can.create_oval(110,210, 190, 290, outline="red")
        elif col == 2 :
            if line == 0:
                can.create_oval(210,10,290,90, outline="red")
            elif line == 1:
                can.create_oval(210, 110, 290, 190, outline="red")
            else :
                can.create_oval(210,210, 290, 290, outline="red")

def verifWin():
    global winner
    if winner == 0:
        for i in range(0,3) :
            if grid[i][0] == grid[i][1] and grid[i][1] == grid[i][2]:
                winner = grid[i][0]
                break
        for i in range(0,3) :
            if grid[0][i] == grid[1][i] and grid[1][i] == grid[2][i]:
                winner = grid[0][i]
                break
        if (grid[0][0] == grid[1][1] and grid[1][1] == grid[2][2]) or (grid[0][2] == grid[1][1] and grid[1][1] == grid[2][0]) :
            winner = grid[1][1]

    if winner ==  0:
        print("match nul")
    else :
        print(str(winner), "a gagné")


def newGame():
    global grid, player, winner
    can.delete(ALL)
    grid = [
        [0, 0, 0],
        [0, 0, 0],
        [0, 0, 0]
    ]
    drawLines()
    player = True
    winner = 0


player = True
winner = 0
grid = [
    [0, 0, 0],
    [0, 0, 0],
    [0, 0, 0]
]

fen = Tk()

can = Canvas(fen, width=300, height=300, bg="white")
can.bind('<Button-1>', pointeur)
can.grid(column=0, row=0, columnspan=2)

drawLines()

Button(fen, text="Quitter", command=quit).grid(column=0, row=1)

Button(fen, text="Reset", command=newGame).grid(column=1, row=1)


fen.mainloop()
fen.destroy()
