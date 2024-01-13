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
