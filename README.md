import random


class Player(object):
    global amount_bet
            
    def __init__(self):
        print "We have a new player!"
        print ""
        self.get_name_player()
    
    def get_name_player(self):
        name = self.set_name_player()
        return name
        
    
    def set_name_player(self):
        name_player = raw_input("What is your name?")
        self.start_blackjack()
        return name_player
    
    def start_blackjack(self):
        while True:
            try: 
                answer = raw_input("Do you want to play to Blackjack?")
                if answer == "yes" or answer == "Yes" or answer == "YES":
                    # Instatiate Deck class and call shuffle_deck method
                    print
                    self.get_amount_bet()
                    break
                elif answer == "no" or answer == "No":
                    print "Shame, come back whenever you want to play!"
                    break
                else:
                    print "You can only reply by yes or no!"
                    continue
            except:
                print "We are in the except step!"
                continue
            finally:
                pass
        
        
    
    def get_amount_bet(self):
        amount_bet = self.set_amount_bet()
        deck.shuffle_deck()
        
    
    def set_amount_bet(self):
        while True:
            try:
                amount_bet = int(raw_input("How much do you want to bet for?"))
                print "Your bet is £%d" % amount_bet
                print
                break
                return amount_bet
            except:
                print "Looks like you did not enter an integer"
                continue
            finally:
                pass


#     TO BE FIXED!!
    def stand(self):
        while True:
            try:
                answer_stand = raw_input("What do you want to do, HIT or STAND?")
                if answer_stand == "stand" or answer_stand == "Stand" or answer_stand == "STAND":
                    if total_val_cards_dealer < total_val_cards_player:
                        print "You have won %r, you win an extra £%d" % (name_player, amount_bet)
                        break
                    elif total_val_cards_dealer == total_val_cards_player:
                        print "It is a draw %s, you can keep your £%d" % (name_player,amount_bet)
                        break
                    else:
                        print "Dealer has won, you loose £%d, %s" % (amount_bet,name_player)
                        break
                else:
                    pass
            except:
                print "You can only choose between HIT and STAND!"
                continue
            finally:
                pass
    
    def prt(self):
        print "This is a test of the prt method in Player class!"
        
    def double_down(self):
        while True:
            try:
                answer_double = raw_input("Do you want to double down?")
                if answer_double == "yes" or answer_double == "Yes" or answer_double == "YES":
                    amount_bet += amount_bet
                    print "Amount bet is %d" % amount_bet
#                     Get a 3rd card
                    name_card3_player = deck.cards.get_name_card(deck[4])
#                     Get value of 3rd card
                    val_card3_player = deck.cards.get_val_card2(name_card3_player)
                else:
                    pass
            except:
                pass
            finally:
                pass
                    
#                     TO BE FINISHED
                    
            
        

class Cards(object):
    
    # class attribute
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
                "Ace of Clubs", "Ace of Diamonds", "Ace of Hearts", "Ace of Spades")
    
    def __init__(self):
        pass
        
    def get_name_card(self,num):
        name_card = self.card_lst[num]
        print "With deck number %d, card is %r" %(num, name_card)
        print
        return name_card


class Deck(object):
    
    # class attribute
    cards = Cards()
    
    
    
    def __init__(self):
        print "Welcome to Itrisso N'gouzo's Blackjack"
        print
        print "A new deck of 52 cards has just been created!"
        print
        
    def shuffle_deck(self):
        global deck
        deck = range(1,49)
        random.shuffle(deck)
        print "Shuffled deck is %r" % deck
        print ""
        # Call get_name_cards method for the first 4 cards
        
        global name_card1_player
        global name_card2_player
        global name_card1_dealer
        global name_card2_player
        global name_card2_dealer
        
        name_card1_player = self.cards.get_name_card(46)
        name_card1_dealer = self.cards.get_name_card(deck[1])
        name_card2_player = self.cards.get_name_card(deck[2])
        name_card2_dealer = self.cards.get_name_card(deck[3])
        #name_card3_player = self.cards.get_name_card(deck[4])
        global val_card1_player
        global val_card2_player
        global val_card1_dealer
        global val_card2_dealer
        
        self.get_val_card2(name_card1_player)
        val_card1_player = val_card
        
        self.get_val_card2(name_card2_player)
        val_card2_player = val_card
        
        self.get_val_card2(name_card1_dealer)
        val_card1_dealer = val_card
        
        self.get_val_card2(name_card2_dealer)
        val_card2_dealer = val_card
        
#         get total value for cards
        self.get_total_val_cards()

#         Call stand method
#         self.player.prt()
        
        return deck
    
    def get_val_card2(self,card):
        while True:
            global val_card
            try:
                val_card = int(card.split()[0])
                if 2 <= val_card <= 9:
                    print "Value of %r is %d" % (card,val_card)
                    print
                    return val_card
                    break    
            except:
                try:
                    val_card = card.split()[0]
                    if val_card == "Ace":
                        self.get_val_Ace(card)
                        print "We are now out of the loop, val Ace is %d" % val
                        break
                    else:
                        val_card = 10
                        print "You have %r, it's value is %d!" % (card, val_card)
                        print
                        return val_card
                        break
                except:
                    break
                    pass
                finally:
                    pass
            finally:
                pass
#     VAL OF ACE IS LOST, NEED TO FIND A WAY TO RETURN IT!!        
    def get_val_Ace(self, card):
        while True:
            try:
                val_card = int(raw_input("Which value do you want for your Ace, 1 or 11?"))
                if val_card == 1:
                    print "Your %s has a value of %d" % (card, val_card)
                    print
                    break
                    return val_card
                    
                elif val_card == 11:
                    print "Your %s has a value of %d" % (card, val_card)
                    print
                    print "We are still in the get_val_Ace loop Ace's val is %d" % val_card
                    break
                    return val_card     
            except:
                print "Your Ace's value can only be 1 or 11!"
                continue
            finally:
                pass
        
          
    def get_total_val_cards(self):
        global total_val_cards_player
        global total_val_cards_dealer
        total_val_cards_player= val_card1_player + val_card2_player
        total_val_cards_dealer= val_card1_dealer + val_card2_dealer
        print "Total value cards for player is %d" % total_val_cards_player
        return total_val_cards_player,total_val_cards_dealer
        

class Dealer(object):
    
    def __init__(self):
        pass
        
    def distribute_cards(self):
        pass

        
# Declare global1 methods outside of ALL classes!!
global deck
deck = Deck()
global player
player = Player()


