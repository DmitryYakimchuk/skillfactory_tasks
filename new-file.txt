# Tic-tac-toe game

def game():


    def print_field(game_field):
        """Функция печатает текущее поле игры"""
        #New comment
        for line in game_field:
            for each in line:
                print(each, end="")
            print()


    # Генерация пустого поля игры
    field = [ [] for i in range(4)]
    for line in field:
        line.append(" – ")
        line.append(" – ")
        line.append(" – ")
        line.append(" – ")

    # Нумерация столбцов и строк
    field[0][0] = "   "
    field[0][1] = "1  " # Нумерация столбцов
    field[0][2] = "2  "
    field[0][3] = "3  "
    field[1][0] = "1 " # Нумерация строк
    field[2][0] = "2 "
    field[3][0] = "3 "

    print_field(field)  # Вывод начального игрового поля

    attemp = 0 # Объявляем начальное количество ходов в игре

    while attemp < 9:
        # Определяем какому игроку ходить, "крестикам" или "ноликам"
        if attemp % 2 == 0:
            move = ' x '
        else:
            move = ' 0 '
        print(f'Ходит игрок, который расставляет {move}.')

        # Определяем местоположение "x" или "0", а также корректность местоположения
        i = int(input(f'Введите номер строки от 1 до 3, куда следует поместить {move}: '))
        j = int(input('А теперь номер столбца, также от 1 до 3: '))
        if not(1<=i<=3) or not(1<=j<=3):
            print('Вы ввели некорректный номер строка-столбец. Повторите ввод.')
            continue

        if field[i][j] != " x " and field[i][j] != " 0 ": # Проверяем не занято ли выбранное место уже " x " или " 0 "
            field[i][j] = move # Помещаем " х " или " 0 " в выбранное положение
            attemp += 1 # Увеличиваем количество ходов в игре
            print('Теперь игроевое поле выглядит так: ')
            print_field(field)

            """Проверка победителя"""
            # Проверка победителя по строкам
            for line in field:
                count_line = 0
                for column in line:
                    if move == column: count_line += 1
                if count_line == 3:
                    print(f"Игра окончена. Выиграл игрок, расставлявший '{move.replace(' ', '')}'.")
                    return print('Конец игры.')

            # Проверка победителя по столбцам
            columns = 1
            while columns <= 3: # Проходим по столбцам
                count_move_in_column = 0
                lines = 1
                while lines <= 3: # Проходим по строкам
                    if move == field[lines][columns]: count_move_in_column += 1
                    if count_move_in_column == 3:
                        print(f"Игра окончена. Выиграл игрок, расставлявший '{move.replace(' ', '')}'.")
                        return print('Конец игры.')
                    lines += 1
                columns += 1

            # Проверка победителя по диагоналям
            if field[1][1] == field[2][2] == field[3][3] != " – " or field[1][3] == field[2][2] == field[3][1] != " – ":
                print(f"Игра окончена. Выиграл игрок, расставлявший '{move.replace(' ', '')}'.")
                return print('Конец игры.')

        else:
            print('Это поле уже занято. Попробуйте снова.')
            continue
    return print('Все свободные поля заняты.\nИгра завершена. Ничья.')


start = input('Введите Y – для начала игры, или любую другую клавишу – для выхода из игры: ')

if start == 'Y':
    game()
else:
    print('Пока.')
