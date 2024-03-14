game_pole = [1, 2, 3, 4, 5, 6, 7, 8, 9]
game_zone = 3

def game_area():
    print("_" * 4 * game_zone)
    for i in range(game_zone):
        print((" " * 3 + '|')*3)
        print('',game_pole[i*3], '|', game_pole[1+i*3],'|', game_pole[2+i*3], '|')
        print(("_" * 3 + '|') * 3)

def game_step(step_game, char):
    if (step_game > 9 or step_game < 1 or game_pole[step_game-1] in ('X' , 'O')):
        return False
    game_pole[step_game - 1] = char
    return True

def game_win():
    win = False

    win_combination = (
        (0,1,2), (3,4,5), (6,7,8),
        (0,3,6), (1,4,7), (2,5,8),
        (0,4,8), (2,4,6)
    )

    for comb in win_combination:
        if (game_pole[comb[0]] == game_pole[comb[1]] and game_pole[comb[1]] == game_pole[comb[2]]):
            win = game_pole[comb[0]]
    return win

def start_game():
    step_player = "X"
    step = 1
    game_area()
    while (step < 10) and (game_win() == False):
        step_game = input('Ходит игрок ' + step_player + '! Введите номер поля')
        if (game_step(int(step_game), step_player)):
            print("Удачный ход")

            if(step_player == 'X'):
                step_player = "O"
            else:
                step_player = "X"
                
            game_area()
            step += 1
        else:
            print("Поле занято! Выберете другое")
    if (step == 11):
        print("Ничья!")
    else:
        print('Победил ' + game_win() + '!')

print('Добро пожаловать в "Крестики-нолики"')
start_game()
