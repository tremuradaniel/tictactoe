def tic_tac_toe():
    from IPython.display import clear_output
    player_x = {'start': [0], 'movesx': [], 'name': 'Player x', 'vic': [0]}
    player_0 = {'start' : [0], 'moves0': [], 'name': 'Player 0', 'vic': [0]}
    win_l = [(1, 4, 7), (2, 5, 8), (3, 6, 9), (1, 2, 3), (4, 5, 6), (7, 8, 9), (1, 5, 9), (3, 5, 7)]  
    available_moves = {'am': [1, 2, 3, 4, 5, 6, 7, 8, 9]}
    moves = {'m': []}
    def introduction():
        """
        This function will greet the users
        """
        greetings = input('Would you like to play a game? You may answer using y or n')
        if greetings == 'y':
            clear_output()
            print('Very well, let us begin!')
        elif greetings == 'n':
            clear_output()
            print("Then don't waste my bloody time!")
        elif greetings != 'y' and greetings != 'n':
            clear_output()
            print('I already said that it is a y or no question... let us try again!')
            return introduction()
    def first_to_start():
        """
        Randomly pick 0 or x to start the game
        """
        from random import randint
        first = randint(0, 1)
        if first == 1:
            player_x['start'] = 1
            print(player_x['name'] + ' will start the game')
        else:
            player_0['start'] = 1
            print(player_0['name'] + ' will start the game')
    def restart_game():
        restart = input('Would you like to play again?')
        if restart == 'y':
            return first_to_start()
        elif restart == 'n':
            clear_output()
            player_x['vic'] = 1
            player_0['vic'] = 1
            print('Have a nice day!')
        else:
            print('Please answer with y or no')
            return restart_game()
    def draw():
        if (len(player_x['movesx']) == 5 and len(player_0['moves0']) == 4) or (len(player_x['movesx']) == 4 and len(player_0['moves0']) == 5):
            print('We have a draw!')
            return restart_game()
        else:
            pass
    def victory():
        for pairs in win_l:
            if set(pairs) <= set(player_x['movesx']) or set(pairs) <= set(player_0['moves0']):
                print('We have a winner!')
                return restart_game()
            else:
                pass
    def users_input():
        table = '''
         _________________
        |     |     |     |
        |  1  |  2  |  3  |
        |_____|_____|_____|
        |     |     |     |
        |  4  |  5  |  6  |
        |_____|_____|_____|
        |     |     |     |
        |  7  |  8  |  9  |
        |_____|_____|_____|
        '''
        print('Please observe the table below', table)
        if player_x['start'] == 1: # start inputing from the user decided in function first_to_start 
            while True:
                # the 2 lines below helps break the loop above when the user do not want to restart the game
                if player_x['vic'] == 1 or player_0['vic'] == 1:
                    break
                while True:
                    movex = int(input(player_x['name'] + ', please chose a number '))
                    moves['m'].append(movex) 
                    if movex in range(1, 10) and set(moves['m']) <= set(available_moves['am']):
                        break
                        #the two lines above are exception: 1. input between 1 and 9, 2. avoid inputing the same numbers
                    else:
                        print('Please pay more attention to the board game')
                        moves['m'].remove(movex) # needed for exception 2. above
                        continue
                clear_output()
                table = table.replace(str(movex), 'x')
                print(table)
                player_x['movesx'].append(movex)
                moves['m'].remove(movex)
                available_moves['am'].remove(movex)
                victory()               
                draw()
                if player_x['vic'] == 1 or player_0['vic'] == 1:
                    break
                while True:
                    move0 = int(input(player_0['name'] + ', please chose a number '))
                    moves['m'].append(move0)
                    if move0 in range(1, 10) and set(moves['m']) <= set(available_moves['am']):
                        break
                        #the two lines above are exception: 1. input between 1 and 9, 2. avoid inputing the same numbers
                    else:
                        print('Please pay more attention to the board game')
                        moves['m'].remove(move0) # needed for exception 2. above
                        continue
                clear_output()
                table = table.replace(str(move0), '0')
                print(table)
                player_0['moves0'].append(move0)
                moves['m'].remove(move0)
                available_moves['am'].remove(move0)
                victory()
        elif player_0['start'] == 1: # start inputing from the user decided in function first_to_start
            while True:
                # the 2 lines below helps break the loop above when the user do not want to restart the game
                if player_x['vic'] == 1 or player_0['vic'] == 1:
                    break
                while True:
                    move0 = int(input(player_0['name'] + ', please chose a number '))
                    moves['m'].append(move0) # line useful for set(moves['m']) <= set(available_moves['am']) below 
                    if move0 in range(1, 10) and set(moves['m']) <= set(available_moves['am']):
                        break
                        #the two lines above are exception: 1. input between 1 and 9, 2. avoid inputing the same numbers
                    else:
                        print('Please pay more attention to the board game')
                        moves['m'].remove(move0) # needed for exception 2. above
                        continue
                clear_output()
                table = table.replace(str(move0), '0')
                print(table)
                player_0['moves0'].append(move0)
                moves['m'].remove(move0)
                available_moves['am'].remove(move0)
                victory()               
                draw()
                if player_x['vic'] == 1 or player_0['vic'] == 1:
                    break
                while True:
                    movex = int(input(player_x['name'] + ', please chose a number '))
                    moves['m'].append(movex)
                    if movex in range(1, 10) and set(moves['m']) <= set(available_moves['am']):
                        break
                        #the two lines above are exception: 1. input between 1 and 9, 2. avoid inputing the same numbers
                    else:
                        print('Please pay more attention to the board game')
                        moves['m'].remove(movex) # needed for exception 2. above
                        continue
                clear_output()
                table = table.replace(str(movex), 'x')
                print(table)
                player_x['movesx'].append(movex)
                moves['m'].remove(movex)
                available_moves['am'].remove(movex)
                victory()
    introduction()
    first_to_start()
    users_input()
tic_tac_toe()    
