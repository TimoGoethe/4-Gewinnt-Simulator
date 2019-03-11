import random
import time
import copy


def main():
    player = []
    x = ""
    print("Enter the names of the players one by one. Enter \"stop\" when you're done.\n")
          #"If it's a Bot, add \"B\" at the Beginning of the name\n")

    while x != "stop":
        x = input("Enter the name of the next player: ")
        if x != "stop":
            player.append(x)
    modi_all(player)
    #modi_ko(player)


def modi_ko(player):
    random.shuffle(player)
    if len(player) > 8:
        cut = len(player) // 2
        players1 = []
        players2 = []
        for i in range(0, cut):
            players1.append(player[i])
        print("group 1:", players1)
        for i in range(cut, len(player)):
            players2.append(player[i])
        print("group 2:", players2)
        result1 = modi_all(players1)
        result2 = modi_all(players2)
        final_players = []
        for i in range(0,4):
            final_players.append(result1[i][1])
            final_players.append(result2[i][1])
        #print(final_players)
        modi_ko2(final_players)

    elif len(player) == 8:
        modi_ko2(player)

    elif len(player) > 4:
        cut = len(player) // 2
        players1 = []
        players2 = []
        for i in range(0, cut):
            players1.append(player[i])
        print("group 1:", players1)
        for i in range(cut, len(player)):
            players2.append(player[i])
        print("group 2:", players2)
        result1 = modi_all(players1)
        result2 = modi_all(players2)
        final_players = []
        for i in range(0, 2):
            final_players.append(result1[i][1])
            final_players.append(result2[i][1])
        print(final_players)
        modi_ko2(final_players)

    if len(player) == 4:
        modi_ko2(player)

    if len(player) < 4:
        print("Sorry, this mode is only available if there are at least 4 player.")

def modi_ko2(players):

    while len(players) > 1:
        #print(players)
        final_players = []
        for i in range(0, len(players), 2):
            #print(len(players))
            #print(players)
            if len(players) == 16:
                print("\n"*20)
                print("###############################")
                print("round of 16")
                print("###############################")
                print("\n")
            if len(players) == 8:
                print("\n"*20)
                print("###############################")
                print("round of 8")
                print("###############################")
                print("\n")
            if len(players) == 4:
                print("\n"*20)
                print("###############################")
                print("semi-final")
                print("###############################")
                print("\n")
            if len(players) == 2:
                print("\n"*20)
                print("###############################")
                print("final")
                print("###############################")
                print("\n")
            result = match([players[i], players[i+1]])
            while len(result[0]) != 1: #kein Gewinner
                result = match([players[i], players[i + 1]])
            final_players.append(result[0][0])
        players = final_players
    print("And the winner is:", final_players[0])


def modi_all(player, iterations=1):

    games = []
    for i in player:
        for j in player:
            if (i != j):
                if ([str(j), str(i)]) in games:
                    pass
                else:
                    for k in range(0, iterations):
                        games.append([i, j])

    # print(games)
    points = []
    for i in player:
        points.append([0, i])

    random.shuffle(games)
    for i in range(0, len(games)):
        # print("i", i)
        x = random.randint(0, 1)
        # print("old", games[i])
        if x == 1:
            games[i] = [games[i][1], games[i][0]]
            # print("new", games[i])
    print(games)
    any_input = input("Start")

    # Play all games and record points
    for i in games:
        result = match(i)  # match(i) is the game
        for j in points:
            try:
                if j[1] == result[0][0]:
                    j[0] += 3
            except IndexError:
                pass
            try:
                if j[1] == result[1][0]:
                    j[0] += 1
                if j[1] == result[1][1]:
                    j[0] += 1
            except IndexError:
                pass

        points.sort()
        points.reverse()
        rank = 1
        for person in points:
            print(str(rank) + ".", person[1], "with", person[0], "points")
            rank += 1
    return points




def match(x):
    print(x[0], "vs.", x[1], "\n")
    any_input = input("Start")

    game_over = False
    result = [[], [], []] # first list: 3p, second: 1p, third: 0p
    game_state = []
    # every sub-list is a column
    for i in range(0,9):
        game_state.append([])
    game_state2 = copy.deepcopy(game_state)
    for i in range(0,9):
        for j in range(0,9):
            game_state[i].append("-")
            game_state2[i].append(" - ")

    last_stone = -1
    while game_over == False:
        for i in range(0,2): #it's player i's turn
            #time.sleep(1)
            valid_input = False
            count_invalid_input = 0
            while valid_input == False and game_over == False:
                count_stones = 0
                for ii in range(0,9):
                    for jj in range(0,9):
                        if game_state[ii][jj] != "-":
                            #print("there is a stone")
                            count_stones += 1

                #print("####", x[i])
                try:
                    chosen_column = eval(x[i])(game_state, count_stones, last_stone)
                except:
                    chosen_column = 19
                    count_invalid_input += 1
                if count_invalid_input > 20:
                    chosen_column = random.randint(0,8)
                if type(chosen_column) == int:
                    try:
                        for j in range(0,9):
                            if game_state[chosen_column][j] == "-":
                                #print(game_state[chosen_column][j])
                                game_state[chosen_column][j] = 15
                                game_state2[chosen_column][j] = " " + str(i) + " "
                                valid_input = True
                                last_stone = chosen_column
                                break
                            else:
                                count_invalid_input += 1
                    except:
                        pass


            output = []
            for i in range(0,9):
                output.append([])

            for i in range(0,9):
                for j in range(0,9):
                    output[i].append(game_state2[j][i])

            if "ss" in any_input:
                time.sleep(5)
            if "st" in any_input:
                time.sleep(3)
            if "s" in any_input:
                print("0:", x[0])
                print("1:", x[1])
                print("\n")

                for i in range(8, -1, -1):
                    print(output[i])
                print("   0      1      2      3      4      5      6      7      8")




            for s in range(0,9):
                for t in range(0, 9):
                    if game_state[s][t] == 15:
                        game_state[s][t] = 16
                    elif game_state[s][t] == 16:
                        game_state[s][t] = 15

            current = check(game_state)
            game_over = current[0]
            winner = current[1]

    if winner == False:
        result[1].append(x[0])
        result[1].append(x[1])
        print("\n", "There is a draw between", x[0], "and", x[1])
        #time.sleep(2)
    if winner == 15:
        result[0].append(x[0])
        result[2].append(x[1])
        print("\n", x[0], "wins against", x[1], "\n")
        #time.sleep(2)
    if winner == 16:
        result[0].append(x[1])
        result[2].append(x[0])
        print("\n", x[1], "wins against", x[0])
        #time.sleep(2)

    return(result)


def check(game_state):
    game_over = False
    winner = False
    for i in range(0, 9):
        for j in range(0, 9):
            try:
                if game_state[i][j] != "-":

                    # 1
                    if game_state[i][j] == game_state[i][j + 1]:
                        if game_state[i][j] == game_state[i][j + 2]:
                            if game_state[i][j] == game_state[i][j + 3]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i][j - 1]:
                        if game_state[i][j] == game_state[i][j + 1]:
                            if game_state[i][j] == game_state[i][j + 2]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i][j - 2]:
                        if game_state[i][j] == game_state[i][j - 1]:
                            if game_state[i][j] == game_state[i][j + 1]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i][j - 3]:
                        if game_state[i][j] == game_state[i][j - 2]:
                            if game_state[i][j] == game_state[i][j - 1]:
                                winner = game_state[i][j]
                                game_over = True

                    # 2
                    if game_state[i][j] == game_state[i + 1][j]:
                        if game_state[i][j] == game_state[i + 2][j]:
                            if game_state[i][j] == game_state[i + 3][j]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 1][j]:
                        if game_state[i][j] == game_state[i + 1][j]:
                            if game_state[i][j] == game_state[i + 2][j]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 2][j]:
                        if game_state[i][j] == game_state[i - 1][j]:
                            if game_state[i][j] == game_state[i + 1][j]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 3][j]:
                        if game_state[i][j] == game_state[i - 2][j]:
                            if game_state[i][j] == game_state[i - 1][j]:
                                winner = game_state[i][j]
                                game_over = True

                    # 3
                    if game_state[i][j] == game_state[i + 1][j + 1]:
                        if game_state[i][j] == game_state[i + 2][j + 2]:
                            if game_state[i][j] == game_state[i + 3][j + 3]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 1][j - 1]:
                        if game_state[i][j] == game_state[i + 1][j + 1]:
                            if game_state[i][j] == game_state[i + 2][j + 2]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 2][j - 2]:
                        if game_state[i][j] == game_state[i - 1][j - 1]:
                            if game_state[i][j] == game_state[i + 1][j + 1]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 3][j - 3]:
                        if game_state[i][j] == game_state[i - 2][j - 2]:
                            if game_state[i][j] == game_state[i - 1][j - 1]:
                                winner = game_state[i][j]
                                game_over = True

                    # 4
                    if game_state[i][j] == game_state[i + 1][j - 1]:
                        if game_state[i][j] == game_state[i + 2][j - 2]:
                            if game_state[i][j] == game_state[i + 3][j - 3]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 1][j + 1]:
                        if game_state[i][j] == game_state[i + 1][j - 1]:
                            if game_state[i][j] == game_state[i + 2][j - 2]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 2][j + 2]:
                        if game_state[i][j] == game_state[i - 1][j + 1]:
                            if game_state[i][j] == game_state[i + 1][j - 1]:
                                winner = game_state[i][j]
                                game_over = True
                    if game_state[i][j] == game_state[i - 3][j + 3]:
                        if game_state[i][j] == game_state[i - 2][j + 2]:
                            if game_state[i][j] == game_state[i - 1][j + 1]:
                                winner = game_state[i][j]
                                game_over = True

            except IndexError:
                pass

    game_over2 = True
    for i in range(0,9):
        if game_state[i][8] == "-":
            game_over2 = False

    if game_over2 == True:
        game_over = True

    #print([game_over, winner])
    return([game_over, winner])


# first parameter: game_state, the cells with the number 15 contain your own stones,
# cells with 16 contain your oponents stones. Empty cells are initialised with "-"
# second parameter: number of stones
# third parameter: last stone
# it's a 9x9 board, you have to return an integer value between 0 and 8 (range(0,9))


def timo(game_state, y, z):
    return 2

def maria(game_state, y, z):
    return 3

def fritz(game_state, y, z):
    return z+1

def max(game_state, y, z):
    chosen_column = random.randint(0,8)
    return chosen_column

def fernando(game_state, y, z):
    if y < 8:
        return y
    else:
        return 4

def strategy(game_state, y, z):
    need = False
    need_column = 0
    for i in range(0, 9):
        top = 0
        for j in range(0, 9):
            if game_state[i][j] != "-":
                top = j
        if game_state[i][top] == 16:
            try:
                if game_state[i][top - 1] == 16:
                    if game_state[i][top - 2] == 16:
                        need = True
                        need_column = i
            except:
                pass

    if need == True:
        return need_column
    else:
        if game_state[4][8] == "-":
            return 4
        elif game_state[5][8] == "-":
            return 5
        elif game_state[6][8] == "-":
            return 6
        elif game_state[7][8] == "-":
            return 7
        else:
            return 8


main()
