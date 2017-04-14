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

import random
class Card_deck(object):
  # Class objects
  suit = ['diamonds', 'clubs','hearts','spades']
  value = ['Ace', '2','3','4','5','6','7','8','9','10','Jack','Queen','King']
  rank = {'2':2, '3':3, '4':4, '5':5, '6':6, '7':7, '8':8, '9':9,
              'Jack': 10, 'Queen':10, 'King':10, 'As':11}

  def __init__(self):
    print "A deck of 52 cards has been created!"


  def draw_cards(self):

  # Pick 2 random cards for each player among 52 cards and display one card for each player
    # Create global arguments
    global card1_player
    global card2_player
    global card1_dealer
    global card2_dealer
    # Randomly select 4 cards in the deck and assign 2 cards for player and for dealer. Needs to find a way no to select the         same cards!
    ranks = random.sample(Card_deck.rank, 4)
    suits = random.sample(Card_deck.suit, 4)
    card1_player = [ranks[0] + " of " +suits[0]]
    card2_player = [ranks[1] + " of " +suits[1]]
    card1_dealer = [ranks[2] + " of " +suits[2]]
    card2_dealer = [ranks[3] + " of " +suits[3]]
    print "Player has %s and another card" % random.choice((card1_player,card2_player))
    print "Dealer has %s and another card" % random.choice((card1_dealer,card2_dealer))
    return card1_player, card2_player, card1_dealer, card2_dealer
    


