import random
class Card_deck(object):
    
    
    # Class object

    card_lst = ("Null","2 of Clubs", "2 of Diamonds", "2 of Hearts", "2 of Spades",
                "3 of Clubs", "3 of Diamonds", "3 of Hearts", "3 of Spades",
                "4 of Clubs", "4 of Diamonds", "4 of Hearts", "4 of Spades",
                "5 of Clubs", "5 of Diamonds", "5 of Hearts", "5 of Spades",
                "6 of Clubs", "6 of Diamonds", "6 of Hearts", "6 of Spades",
                "7 of Clubs", "7 of Diamonds", "7 of Hearts", "7 of Spades",
                "8 of Clubs", "8 of Diamonds", "8 of Hearts", "8 of Spades",
                "9 of Clubs", "9 of Diamonds", "9 of Hearts", "9 of Spades",
                "Jack of Clubs", "Jack of Diamonds", "Jack of Hearts", "Jack of Spades",
                "Queen of Clubs", "Queen of Diamonds", "Queen of Hearts", "Queen of Spades",
                "King of Clubs", "King of Diamonds", "King of Hearts", "King of Spades",
                "Ace of Clubs", "Ace of Diamonds", "Ace of Hearts", "Ace of Spades",
                "1 of Clubs", "1 of Diamonds", "1 of Hearts", "1 of Spades")

    def __init__(self):
        print "A new deck of 52 cards has just been created!"
        print

    def shuffle_deck(self):
        global deck
        deck = range(1,49)
        random.shuffle(deck)
        print
        print "Shuffled deck is %r" % deck
        print
            
            
    
            
    # On the first round, select the first 4 cards from the deck        
    def name_cards(self):
        global name_card1_player
        global name_card1_dealer
        global name_card2_player
        #global name_card2_dealer
        
        name_card1_player = Card_deck.card_lst[deck[0]]
        name_card1_dealer = Card_deck.card_lst[deck[1]]
        name_card2_player = Card_deck.card_lst[deck[2]]
        #name_card2_dealer = Card_deck.card_lst[deck[3]]
        
        print "Card1_player is %r" % name_card1_player
        print ""
        print "Card1_dealer is %r" % name_card1_dealer
        print ""
        print "Card2_player is %r" % name_card2_player
        print ""
        
        #print "Card2_player is %r" % name_card2_dealer
        '''picked_cards = [name_card1_player,name_card1_dealer, 
                        name_card2_player,name_card2_dealer]'''
        #print "Your picked cards are: %r" % picked_cards
        
        cards_player = []
        cards_player.append(Card_deck.card_lst[deck[0]])
        cards_player.append(Card_deck.card_lst[deck[2]])
        print "Player's cards are %r" % cards_player
        return cards_player
        
        
    
            
    def assign_val_cards(self, num):
    # Round 1
    # If card's number is between 1 and 32, val_card = first letter of card's name
        
        global deck_first_round
        global val_card
        deck_first_round = deck[0:4]
        
        
        if 1 <= num <= 32:
            
            
            
            #print "Your card number is %d and it is %r" % (num, Card_deck.card_lst[num])
            # Split names of the cards
            split_letter_cards = Card_deck.card_lst[num].split()
            val_card = int(split_letter_cards[0])
            
            #print "Your cards' value is %d" % val_card
            return val_card
            print
        elif 33 <= num <= 44:
            
            
            #print "Your card number is %d and it is %r" % (num, Card_deck.card_lst[num])
            val_card = 10
            #print "Your cards' value is %d" % val_card
            return val_card
            print
            
        elif 45 <= num <= 48:
            
            # Ask the player which value for the Ace, 1 or 11?
            while True:

                try:
                    
                    val_card = int(raw_input("Which value do you want for your Ace, 1 or 11?"))
                    if val_card == 11:
                        global picked_Ace
                        picked_Ace = Card_deck.card_lst[num]
                        print "Your card is %r and has a value of %d" % (picked_Ace, val_card)
                        return val_card
                        print
                        break

                    elif val_card == 1:
                        # Find the One from the name of the Ace
                        if num == 45:
                            picked_One = "1 of Clubs"
                        elif num == 46:
                            picked_One = "1 of Diammonds"
                        elif num == 47:
                            picked_One = "1 of Hearts"
                        else:
                            picked_One = "1 of Spades"
                        print "Your card is %r and has a value of %d" % (picked_One, val_card)
                        return val_card
                        print
                        break

                    else:
                        print "Please enter either 1 or 11 for your Ace's value!"
                        continue
                except:
                    print "Looks like you did not enter an integer\nPlease choose between 1 and 11 as a value for your Ace!"
                    continue
                finally:
                    pass

        else:
            pass
        
    def hit(self):
    # When the player says "HIT", he/she will get a new card
        while True:
            try:
                hit_answer = raw_input("What do you want to do?")
                if hit_answer == "hit":
                    global name_card3_player
                    name_card3_player = Card_deck.card_lst[deck[4]]
                    print "Your new card is %r" % name_card3_player
                    print
                    Card_deck.assign_val_cards(deck[4])
                    global val_card3_player
                    val_card3_player = val_card
                    print "Your %r has a value of %d" %(name_card3_player, val_card)
                    #total_val_cards_player = total_val_cards_player + val_card3_player
                    #print "Total value cards for %r is %d" % ( name_player,total_val_cards_player)
                    break
                else:
                    print "You can only choose between hit and stand!"
                    continue
            except:
                print "You can only choose between hit and stand!"
                continue
            finally:
                pass
        
        
        
        
    # Following rounds
        

        
class Player(object):
    
    def __init__(self):
        print "We have a new player!"
        
        pass
    
    def name_player(self):
        global name_player
        name_player = raw_input("What is your name?")
        print
        print "Welcome to Itrisso N'gouzo's casino, %r!" % name_player
        player = Player()
        player.start_game()
    
    def start_game(self):
        
        while True:
            try:
                answer = raw_input("Do you want to play Blackjack?") 
                if answer == "yes":
                    print
                    print "The game is about to start %r!" % name_player
                    print
                    # Ask the amount bet
                    blackjack = Blackjack()
                    blackjack.bet()
                    print
                    # Initiate the Card_deck class
                    card_deck = Card_deck()
                    # Shuffle the deck
                    card_deck.shuffle_deck()
                    # Name the cards
                    card_deck.name_cards()
                    # Assign val cards
                    card_deck.assign_val_cards(deck[0])
                    global val_card1_player
                    val_card1_player = val_card
                    #print "Value card1 player is %d" % val_card1_player
                    
                    
                    card_deck.assign_val_cards(deck[1])
                    global val_card1_dealer
                    val_card1_dealer = val_card
                    #print "Value card1 dealer is %d" % val_card1_dealer
                    
                    
                    card_deck.assign_val_cards(deck[2])
                    global val_card2_player
                    val_card2_player = val_card
                    #print "Value card2 player is %d" % val_card2_player
                    
                    
                    card_deck.assign_val_cards(deck[3])
                    global val_card2_dealer
                    val_card2_dealer = val_card
                    #print "Value card2 dealer is %d" % val_card2_dealer
                    
                    global total_val_cards_player
                    global total_val_cards_dealer
                    total_val_cards_player = val_card1_player + val_card2_player
                    total_val_cards_dealer = val_card1_dealer + val_card2_dealer
                    
                    
                    
                    
                    #print "Total value cards of player is %d" % total_val_cards_player
                    #print "Total value cards of dealer is %d" % total_val_cards_dealer
                    # Initiate Card_deck class
                    blackjack = Blackjack()
                    # Call stand function in class Blackjack
                    blackjack.stand()
                    
                    # Call hit function in class Card_deck
                    card_deck.hit()
                    global val_card3_player
                    val_card3_player = val_card
                    total_val_cards_player = total_val_cards_player + val_card3_player
                    print "Total value cards for %r is %d" % ( name_player,total_val_cards_player)
                    
                    
                    return val_card1_player
                    return val_card1_dealer
                    return val_card2_player
                    return val_card2_dealer
                    return total_val_cards_player
                    return total_val_cards_dealer
                    
                    break
                    
                elif answer == "no":
                    print
                    print "Come back any time you would like to give it a try!"
                        
                    break
            except:
                pass
            finally:
                pass

            
            
            
class Blackjack(object):
    
    def __init__(self):
        print "The game is about to start!"
    
    
    # Ask how much he wants to bet


    def bet(self):
        while True:
            try:
                amount_bet = int(raw_input("How much do you want to bet?"))
                print "You are betting for £%d" % amount_bet
                return amount_bet
                break               
            except:
                print "Looks like you did not enter an integer!"
                continue
            finally:
                pass
        action = raw_input("What do you want to do, %?") % name_player
        #if acttion == "stand":
            # CPU needs to check the strongest hand to 21
            #val_cards_CPU = 
    
    
    def stand(self):
        while True:
            try:
                stand_answer = raw_input("What do you want to do?")
                if stand_answer == "stand":
                    if total_val_cards_player > total_val_cards_dealer:
                        print "player has won!"
                        break
                    else:
                        print "House has won!"
                        break
                else:
                    pass
            except:
                print "You can only choose between hit and stand!"
                print
                continue
            finally:
                pass
        
            
        
        #print "This the stand function"
        # When the play says "STAND", CPU compares values between CPU's cards and Players'one
        # If CPU's cards are closer to 21, CPU wins and it get all the money the player has bet
        # Otherwise player gets double the amount of money he/she has bet

    def insurrance(self):
        print "This is the insurrance function"
        # When the CPU's up card is an Ace, the player can take an insurrance
        # Insurance is limited to half of the original bet and pays out 2:1
              
        
    def hit(self):
        # When the player says "HIT", he/she will get a new card
        while True:
            try:
                hit_answer = raw_input("What do you want to do?")
                if hit_answer == "hit":
                    
                    global name_card3_player
                    card_deck = Card_deck()
                    name_card3_player = card_deck.card_lst[deck[4]]
                    print "Your new card is %r" % name_card3_player
                    break
                else:
                    print "You can only choose between hit and stand!"
                    continue
            except:
                print "You can only choose between hit and stand!"
                continue
            finally:
                pass
        
    
    def double_down(self):
        print "This is the double-down function"
        # After receiving the first 2 cards, if the players says "double down", he/she can double the original bet and
        # receive another card. The game stops here and CPU will compare the cards
        
        
        
    
    def split(self):
        print "This will be the split function"
        # If the player's 2 cards hold the same value, he/she is allowed to split it into 2 hands
        # A split become 2 different hands with one bet each. Dealer will hit player with one card on each of the split.
        # Player is not allowed to hit, double-down or split after splitting the first time.
        
        pass
    
    def surrender(self):
        print "This is the surrender function"
        # Surrender is offered when the displayed dealer's card is either an Ace or a 10 value card
        # A player who has surrendered forfeit half of his bet to the house. The round ends and a new round starts.
        pass
        
    
    def push(self):
        print "This is the push function"
        # If both the dealer and the player have the same value cards, it is a push
        # No money changes hands
        pass
        
    
    def payout(self):
        print "This is the payout function"
        # If the player beats the dealer with a higher cards combination, he will receive a 1:1 payout
        # If the player hit "blackjack", he will receive a 3:2 payout (£15 reward for £10 original bet)
        pass
        
    
    
    
