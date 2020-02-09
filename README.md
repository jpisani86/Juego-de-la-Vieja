# Juego-de-la-Vieja
# Reglas generales:
# 2 jugadores en la misma computadora
# El tablero de juego debera aparecer cada vez que un jugador selecciona una movida ('X', 'O')


# Primero desarrolamos como se distribuira la tabla de juego y el mensaje inicial para empezar a jugar.


print('-----------------------El juego de la Vieja-----------------------\n')
print('\t\t\t___|__|___')
print('\t\t\t___|__|___')
print('\t\t\t   |  |   ')
print("por favor selecciona tu simbolo:\n1.Jugador 1->X\n2.Jugador 2->O\n>>")

# Ahora procedemos a definir todas las posibles movidas:

print('\t\t\t_1|_2_|_3__')
print('\t\t\t_4|_5_|_6_')
print('\t\t\t 7| 8 | 9 ')

# Ahora creamos una lista vacia donde se almacenaran todos los movimientos que cada jugador haya realizado

list_jug1= []
list_jug2 = []

# Ahora creamos una lista con todas las posibles movidas que todos los jugadores podran realizar (9 en total + 0):

list = ['', '', '', '', '', '', '', '', '', '']

# La siguiente funcion define con mayor precision el tablero. La funcion tendra 2 parametros: Jugador + input

def Mostrar_tablero(jugador, input):

    print('La jugada es', input)
    ''''''
    print("\t\t\t_", list[1], "_|_", list[2], "_|_", list[3], "_")
    print("\t\t\t_", list[4], "_|_", list[5], "_|_", list[6], "_")
    print("\t\t\t_", list[7], "_|_", list[8], "_|_", list[9], "_")
    
# Ahora crearemos algunas normas generales del juego:
# 1) Asegurarnos de que ningun jugador pueda tomar una posicion ya usada:
# Como hemos definido cada posicion no usada con '', solo tenemos que usar un condicional para verificar si la posicion esta vacia


def Check_seleccion(input_jugador):
    
    if list[input_jugador] == '':
        return True
    else:
        return False
    
# Ahora definimos los escenarios con los que se puede ganar al juego de la vieja:

def ganar(chk):
    return (list[1] == list[2] == list[3] == chk or
            list[4] == list[5] == list[6] == chk or
            list[7] == list[8] == list[9] == chk or
            list[1] == list[4] == list[7] == chk or
            list[2] == list[5] == list[8] == chk or
            list[3] == list[6] == list[9] == chk or
            list[1] == list[5] == list[9] == chk or
            list[7] == list[5] == list[3] == chk)

# Ahora procedemos a definir la funcion central de todo el juego:

def jugar():
        # Definimos la variable list_input de forma que ningun jugador puede seleccionar ninguna movida despues del numero 9
    list_input = 1
   #El codigo de abajo chequea si la posicion ha sido ya tomada
    error_jug2 = 'off'
    while(list_input <= 9):  
        if(list_input % 2 != 0):  
            print('Jugador:X Selecciona tu posicion')
            input_jug1 = int(input(''))  # Guarda la jugada del primer jugador
            #Aqui volvemos a chequear que la posicion no ha sido tomada already.
            if (Check_seleccion(input_jug1)) and (error_jug2 == 'off'):
                # we are assigning the value 'X' ie username in the list,so
                # that it can  be displayed by Function displayBoard()
                list[input_jug1] = "X"
                Mostrar_tablero('X', input_jug1)
                # checking for winner .we supply value 'X' and check whether
                # "x" is winner or not
                if(ganar('X')):
                    print("X es el ganador!!!")
                    break
                    # we increase thelist_input variable so that we know that
                    # on position has been filled
                list_input += 1

            else:  # if position is already taken then  we continue the loop so again beginning from top
                print('La posicion ha sido ya tomada.Selecciona otra posicion X\n`')
                continue
        else:
            # this part runs for evn vaue of list_input
            if(list_input != 9):
                print('Jugador:O Selecciona tu posicion')

                input_jug2 = int(input(''))
                if Check_seleccion(input_jug2):

                    list[input_jug2] = "O"
                    list_jug2.append(input_jug2)
                    if(ganar("O")):
                        print("O es el ganador!!!")
                        break
                    list_input += 1

                    Mostrar_tablero("O", input_jug2)
                    error_jug2 = 'off'

                else:
                    print(
                        'La posicion ha sido ya tomada.Selecciona otra posicion O \n')
                    # here we assign error_pl2 as on so that  for next
                    # iteration we can skip  asking input for player 1.
                    error_jug2 = 'on'
    repeat = input('Quisieras jugar otra vez? S para Si y n para no?::')
    if(repeat == "s" or repeat == "S"):
        jugar()
