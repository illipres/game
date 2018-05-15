# game
ita game
import random


def MainMenu():
    print("Welcome to Battle Arena! This is a turn based combat game where")
    print("only one person will come out alive.")

    print("To play this game you will switch turn making moves which can deal different damage")
    print("there is low range damage punch, medium damage mega kick and also healing")
    print("remember that you can attack and heal, and a chance of missing even the heals")

    print("both you and the AI will start with 100 HP")
    print("the first one to get to 0 will be the winner")
    print("Good luck and may the strongest one come out alive")

    play_again = True

    while play_again:
        winner = None
        player_health = 100
        computer_health = 100

        turn = random.randint(1,2) 
        if turn == 1:
            player_turn = True
            computer_turn = False
            print("Player will go first.")
        else:
            player_turn = False
            computer_turn = True
            print("Computer will go first.")


        print("Player health: ", player_health, "Computer health: ", computer_health)

        
        while (player_health != 0 or computer_health != 0):

            heal_up = False 
            miss = False 

            
            moves = {"Punch": random.randint(18, 25),
                     "Mega Kick": random.randint(10, 35),
                     "Heal": random.randint(20, 25)}

            if player_turn:
                print("Please select a move:\n1. Punch (Deal damage between 18-25)\n2. Mega Kick (Deal damage between 10-35)\n3. Heal (Restore between 20-25 health)")

                player_move = input("> ").lower()

                move_miss = random.randint(1,5) 
                if move_miss == 1:
                    miss = True
                else:
                    miss = False

                if miss:
                    player_move = 0 
                    print("You missed!")
                else:
                    if player_move in ("1", "punch"):
                        player_move = moves["Punch"]
                        print("You used Punch. It dealt ", player_move, " damage.")
                    elif player_move in ("2", "mega Kick"):
                        player_move = moves["Mega Kick"]
                        print("You used Mega Punch. It dealt ", player_move, " damage.")
                    elif player_move in ("3", "heal"):
                        heal_up = True 
                        player_move = moves["Heal"]
                        print("You used Heal. It healed for ", player_move, " health.")
                    else:
                        print("That is not a valid move. Please try again.")
                        continue

            else: 

                move_miss = random.randint(1,5)
                if move_miss == 1:
                    miss = True
                else:
                    miss = False

                if miss:
                    computer_move = 0 
                    print("The computer missed!")
                else:
                    if computer_health > 30: 
                        if player_health > 75:
                            computer_move = moves["Punch"]
                            print("The computer used Punch. It dealt ", computer_move, " damage.")
                        elif player_health > 35 and player_health <= 75:
                            imoves = ["Punch", "Mega Kick"]
                            imoves = random.choice(imoves)
                            computer_move = moves[imoves]
                            print("The computer used ", imoves, ". It dealt ", computer_move, " damage.")
                        elif player_health <= 35:
                            computer_move = moves["Mega Punch"] 
                            print("The computer used Mega Kick. It dealt ", computer_move, " damage.")                       
                    else: 
                        heal_or_fight = random.randint(1,2) 
                        if heal_or_fight == 1:
                            heal_up = True
                            computer_move = moves["Heal"]
                            print("The computer used Heal. It healed for ", computer_move, " health.")
                        else:
                            if player_health > 75:
                                computer_move = moves["Punch"]
                                print("The computer used Punch. It dealt ", computer_move, " damage.")
                            elif player_health > 35 and player_health <= 75:
                                imoves = ["Punch", "Mega Kick"]
                                imoves = random.choice(imoves)
                                computer_move = moves[imoves]
                                print("The computer used ", imoves, ". It dealt ", computer_move, " damage.")
                            elif player_health <= 35:
                                computer_move = moves["Mega Punch"] 
                                print("The computer used Mega Punch. It dealt ", computer_move, " damage.")

            if heal_up:
                if player_turn:
                    player_health += player_move
                    if player_health > 100:
                        player_health = 100
                else:
                    computer_health += computer_move
                    if computer_health > 100:
                        computer_health = 100
            else:
                if player_turn:
                    computer_health -= player_move
                    if computer_health < 0:
                        computer_health = 0 
                        winner = "Player"
                        break
                else:
                    player_health -= computer_move
                    if player_health < 0:
                        player_health = 0
                        winner = "Computer"
                        break

            print("Player health: ", player_health, "Computer health: ", computer_health)

            
            player_turn = not player_turn
            computer_turn = not computer_turn

        

        if winner == "Player":
            print("Player health: ", player_health, "Computer health: ", computer_health)
            print("Congratulations! You have won. You're an animal!!")
        else:
            print("Player health: ", player_health, "Computer health: ", computer_health)
            print("Sorry, but your opponent wiped the floor with you. Better luck next time.")

        print("Would you like to play again?")

        answer = input("> ").lower()
        if answer not in ("yes", "y"):
            play_again = False

MainMenu()
