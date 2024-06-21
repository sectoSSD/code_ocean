
here is the script of a codingame project intended to compete in a competition called "ocean of code".

url: https://www.codingame.com/multiplayer/bot-programming/ocean-of-code

This script is the seconde version of the projet. I made it to improve my level of python programation and that’s why I decided to make it from scratch. It was a bit naive and I realized rather towards the end that 
I would not be among the best if I did not use libraries to allow the codes to go faster. Indeed ocean of code is a turn-based game with a time limit. Full python programming is too slow to play intelligently in the 
allotted time. We need numpy, pandas and perhaps even scikitlearn...

A third version is expected with these solutions and with the use of classes for more efficient code. 

Here is some main concept of the script :

Direction : 'MOVE Direction' is the main action possible in the game. To be read in a two dimensional 
            map each direction are translated in a tuple (x,y) :
            'S' -> [( 0, 1)]
            'N' -> [( 0,-1)]
            'E' -> [( 1, 0)]
            'W' -> [(-1, 0)]
            Because when the 'SILENCE' implied that several directions are possible, directions are put in
            list
Direction path : it's list of direction. There are two direction paths. The fist is build in random_path and 
                 is made to seek what is the better way to choose in a given position according the several 
                 parameters calculatid in evaluate_dir_map(). The second is the real directions taken by the 
                 submarines during the last rounds of the game. It's load in play_map['direction_path'] and run in config_seek_area()
                 to know in wich tile could be the my and the opposite submarine.
seek_area :  Map showing in wich tile a submarine could start or could be according of a direction path.
                 A the start seek_area is the map showing in wich tile the sub could start according to a
                 random generated direction_path (see random_path()). In game loop it is where a submarine could 
                 be according of the last direction it has taken befor. 
***
play_map keys :
Play_map is the most important (and almost unique) place where are compute player information.
Both players have their own play_map which contains all the information about the player's game. 
It is dictionnary containing several types of variable and sequences. 
'who' : 'Me' or 'He'
'status' : 'start' or 'game_loop'
'position' : Tuple (x,y) representing the current position of (x,y) 'None' in his_play_map

'direction_path'       :   List of list of tuples representing directions previously followed by the submarine.
                           [[(0,-1)],[(0,-1)],[(1,0)]] is 'North, North, West'. Sometimes, when the opposit players plays 
                           'Silence' there is several tuples the list of list : [[(0,1)],[(0,1),(0,-1)]]
                           See 'dir_converter' function for all details.
'next_direction'       :   Next direction calculated by 'next_tile' function not yet in 'play_map['direction_path']'.
'seek_area'            :   Tile on the map where the opponent, who desn't know the position could think, the submarine is according to his direction path. 
'next_direction_paths' :  'Next_tiles' function have few time to find à good next tile for the submarine. Keeping
                           the best next_paths of the previus search in 'next_tiles' function ensure us to have a
                           good next direction.            
'max_length_next_path' :   Maximum length of next_path earn in next_tile function. Give idea of the space 
                           that have the submarine to move.           
'direction_path_length'' : Length of direction_path. avoid two employ len(play_map['direction_path']) several times in the game.
'fork'   :                 The list of index of the list of list of 'dir' where there is more than one tuples :
                           [[(0,1)],[(0,1),(0,-1)],[(0,1)],[(0,1),(0,-1)]] give play_map['fork'] = [1,3].
                           Use especially in 'run_path' function.
'sector' :                 Dictionnary of three dictionnaries built in the same way. 'In' contains sector where 
                           submarine must be at a given lap. 'in' : { 0 : 1} mean 'the submarine must be in sector 
                           1 at lap 0' wich correspond also to play_map['direction_path'][0] and play_map['last_tiles'][0] 
                           wich are the index 0 of 'dir' list and 'last_tiles' list.
'last_tiles :             List of tuples representing tiles previously traveled by the submarine'.
                          [(1,2),(1,1),(1,1),(0,0)] when following the 'dir' exemple above.
***
    debug keys :
        'random path' : run best_random_path (), random_path() and value() several time. Print and plot
                        some indicator showing how best direction path is chosen.
        
        'debug_path'  : give graphic view of the direction_path chosen by best_random_path() 
        
        'check_seek_area' : checks adjustement of config_seek_area()
        'debug_map'   : give graphic view of seek_area which show where the sub can be according of
                        the direction_path taken. At start shows wich start tile could be chosen. In game
                        loop where the submarine could be. See more in debug_map()
