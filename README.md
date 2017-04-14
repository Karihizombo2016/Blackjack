# Blackjack
First blackjack game with one player against the dealer

from numpy import random

#Create set of classes
class Player(object):
    
    
    def __init__(self):
        print "A player is created!"
        
    def player_name(self, player_name, player_pot = 10):
        self.player_name = player_name
        self.player_pot = player_pot
        player_name = raw_input("What is your name?")
        print "Welcome to Itrisso's BlackJack %s!" % player_name
        
    def reset_player_pot(self, player_pot):
        pass
        #player_pot = player_pot + win or - loss
        
    def actions(self):
        pass
        # A player can HIT
        # A player can STAND
        # A player can DOUBLE DOWN
        # A player can SPLIT
        # A player can SURRENDER
        # A player can TAKE AN INSURRANCE
    
    def payout(self,bet):
        self.bet = bet
        # If the player has the highest card combination, 1:1 (£10 received for £10 bet)
        # If the player hits "Blackjack" with the 2 cards, He/She will receive 3:2 (£15 for £10 bet)

class Rules(object):
    
    def __init__(self):
        #Print an explication of the blackjack rules

class Dealer(object):
    
    def __init__(self):
        
    def distr_cards(self):
        # A dealer will distribute 2 random cards to the player and 2 random cards to itself
        # One card of each game (player and dealer) will be displayed
        pass

class Card_deck(object):

    # Class object
    colour = ['of diamonds', 'of clubs','of hearts','of spades']
    value = ['As', '2','3','4','5','6','7','8','9','10','Jack','Queen','King']
    value_cards = {'2':2, '3':3, '4':4, '5':5, '6':6, '7':7, '8':8, '9':9,
                  'Jack': 10, 'Queen':10, 'King':10, 'As':11}
    
    def __init__(self):
        print "A deck of 52 cards has been created!"
        
        
    def draw_cards(self):
        
        # Pick 2 random cards amongs the 52 and diplay them
        global card1
        card_name1 = random.choice(Card_deck.value,3)
        card_shape1 = random.choice(Card_deck.colour)
        card_name2 = random.choice(Card_deck.value)
        card_shape2 = random.choice(Card_deck.colour)
        card_name3 = random.choice(Card_deck.value)
        card_shape3 = random.choice(Card_deck.colour)
        card_name4 = random.choice(Card_deck.value)
        card_shape4 = random.choice(Card_deck.colour)
        card1 = [card_name1 +" "+ card_shape1]
        card2 = [card_name2 +" "+ card_shape2]
        card3 = [card_name3 +" "+ card_shape3]
        card4 = [card_name4 +" "+ card_shape4]
        
        print "card1 is %s\ncard2 is %s\ncard3 is %s\ncard4 is %s" % (card1,card2,card3,card4)
        #print "Card2 is %s" % card2
        #print "Card2 is %s" % card2
        return card1, card2, card3, card4
    
    def assign_val_card(self,card1):
        self.card1 = card1
        val_card = 0
        card1 = draw_cards()
        print "Card1 is %s" % card1
        

