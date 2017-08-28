
# Objectives:
#  Change the name input so that even with a space before the name it does still work
#  Restart the game with the rest of the total amount and the following cards on the deck
# When the player stands distribute cards to dealer so that it would get as clause as possible to 21!
# When distributing 1 extra cards, we cannot choose the value of the Ace anymore!!
# Methods to fix
# - Surrender

import random


class Player2(object):
    positive_answer = ["yes", "Yes", "YES"]
    negative_answer = ["no", "No", "NO"]

    def __init__(self):
        pass


class Colour(object):
    # PURPLE = '\033[95m'
    # CYAN = '\033[96m'
    # DARKCYAN = '\033[36m'
    # BLUE = '\033[94m'
    # GREEN = '\033[92m'
    # YELLOW = '\033[93m'
    # RED = '\033[91m'
    BOLD = '\033[1m'
    # UNDERLINE = '\033[4m'
    END = '\033[0m'


class Player(object):

    positive_answer = ["yes", "Yes", "YES"]
    negative_answer = ["no", "No", "NO"]
    # global positive_answer
    # global negative_answer

    def __init__(self):
        print "We have a new player!"
        print ' '
        self.set_name_player()

    def prt_test(self):
        print "Test for Player class"

    def set_name_player(self):
        global name_player
        while True:
            try:
                name = (raw_input("What is your name?\n")).split(' ')
                if name[0] == '':
                    name_player = name[1]
                else:
                    name_player = name[0]
                print "Hi %s!" % name_player
                print
                self.prt_rules()
                return name_player
            except ValueError:
                print "Your name can't be a number only!"
                continue
            finally:
                pass

    def prt_rules(self):

        print colour.BOLD + "Blackjack is played against the house.\n" \
                           "The object of the game is to take cards as close as possible,\n" \
                           "but not exceeding, a value of 21 and beat the dealer's total.\n" \
                           "If, however your hand goes over 21, you are considered to have'busted'\n" \
                           "and will forfeit your bet immediately, regardless of the dealer's hand." + colour.END
        print
        self.start_blackjack()

    def start_blackjack(self):
        global rounds
        while True:
            try:
                answer = raw_input("So, do you still want to play Blackjack?\n")
                if answer in self.positive_answer:
                    rounds = 0
                    print
                    self.set_amount_game()
                    break
                elif answer in self.negative_answer:
                    print "Come back whenever you want to give it a try!"
                    break
            # THIS EXCEPT DOES NOT FUNCTION PROPERLY!!
            except ValueError:
                print "You can only choose between Yes and No!"
                continue
            finally:
                pass

    def set_amount_game(self):
        global amount_game
        while True:
            try:
                amount_game = int(raw_input("How much do you want to put on the table?\n"))
                print u"Your starting amount for the game is \u00a3 % .1f" % amount_game
                print
                self.set_amount_bet(amount_game)
                break
            except ValueError:
                print "Your amount for the game has to be a number!!"
                continue
            finally:
                pass

    def reset_total_amount_game(self, amount_bet, total_amount_game):
        print u"Total amount game \u00a3 %.1f" % total_amount_game
        print u"Amount bet \u00a3 %.1f" % amount_bet

    # ----------------------TO BE TESTED!!!----------------------
    def set_amount_bet(self, amount_game):
        global amount_bet
        global amount_game_left
        if rounds == 1:
            print "we are in round 1!"
            print "Amount game left is %d" % amount_game_left
        else:
            while True:
                try:
                    amount_bet = int(raw_input("How much do you want to bet for?\n"))
                    if amount_game - amount_bet < 0:
                        print u"Your amount bet cannot be smaller than your pot, \u00a3 %d!" % amount_game
                        continue
                    else:
                        print u"Your amount for the game is \u00a3 %.f" % amount_game
                        print u"Your bet is \u00a3 %d" % amount_bet
                        amount_game_left = amount_game - amount_bet
                        print u"You have \u00a3 %d left" % amount_game_left
                        deck.shuffle_deck(amount_bet)
                        break
                except ValueError:
                    print "Looks like you did not enter an integer"
                    continue
                finally:
                    pass


class Cards(object):
    # class attribute
    card_lst = ("Null", "2 of Clubs", "2 of Diamonds", "2 of Hearts", "2 of Spades",
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

    def get_name_card(self, num):
        global name_card
        # print "I am looking for card %d" % num
        name_card = self.card_lst[num]
        # print "With deck number %d, card is %r" % (num, name_card)
        print
        return name_card

    def prt_test(self):
        print "This is the prt test in Cards class"


class Deck(object):
    def __init__(self):
        print
        print "Welcome to Itrisso N'gouzo's Blackjack"
        print
        print "A new deck of 52 cards has just been created."
        print

    def shuffle_deck(self, amount_bet):
        global new_deck
        new_deck = range(40, 49)
        random.shuffle(new_deck)
        print "Shuffled deck is %r" % new_deck
        print
        dealer.distribute_4cards(amount_bet)
        return new_deck, amount_bet

    def get_val_card(self, n, card):
        global val_card
        # print "I am looking for value of card  position %d, which is %s" %(n, card)
        while True:
            try:
                val_card = int(card.split()[0])
                if 2 <= val_card <= 10:
                    # print "Value of %r is %d" % (card, val_card)
                    print
                    break
                    return val_card
            except ValueError:
                try:
                    val_card = card.split()[0]
                    if val_card == "Ace":
                        if n == 1:
                            val_card = 11
                            return val_card
                        elif n == 3 and list_val_cards_dealer[0] != 11:
                            val_card = 11
                            return val_card
                        elif n == 3 and list_val_cards_dealer[0] == 11:
                            print "List val cards dealer %d" % list_val_cards_dealer[0]
                            val_card = 1
                            return val_card
                        else:
                            self.get_val_Ace()
                            # print "The Aces will be dealt later!"
                            # print "We are now out of the loop, val Ace is %d" % val
                            return val_card
                    else:
                        val_card = 10
                        # print "You have %r, it's value is %d!" % (card, val_card)
                        print
                        return val_card
                except ValueError:
                    break
                    pass
                finally:
                    pass
            finally:
                pass

    def get_val_Ace(self):
        global val_card
        while True:
            try:
                val_card = int(raw_input("Which value do you want for your Ace, 1 or 11?\n"))
                if val_card == 1 or val_card == 11:
                    print "Your Ace's value is %d" % val_card
                    print
                    break
                    return val_card
                else:
                    print "Your Ace can only be 1 or 11!"
                    continue
            except ValueError:
                print
                print "Please enter a number, either 1 or 11!"
                continue
            finally:
                pass

    def prt_test(self):
        print "This is the prt test in Deck class"


class Dealer(object):
    positive_answer = ["yes", "Yes", "YES"]
    negative_answer = ["no", "No", "NO"]

    def __init__(self):
        pass

    def distribute_4cards(self, amount_bet):
        global n
        n = 0
        global list_cards_dealer
        global list_cards_player
        global list_val_cards_player
        global list_val_cards_dealer
        list_cards_player = []
        list_cards_dealer = []
        list_val_cards_dealer = []
        list_val_cards_player = []
        # Burn the 1st card
        _ = new_deck.pop(0)
        # print "Discarded card is %r" % list_cards_discarded

        while n < 4:
            # Get the first element of the new deck
            num = new_deck.pop(0)
            # Get the name of the card
            cards.get_name_card(num)
            deck.get_val_card(n, name_card)
            if n % 2 == 0:
                # Append list of player's cards
                list_cards_player.append(name_card)
                # Append list of player's val cards
                list_val_cards_player.append(val_card)
            else:
                # Append list of dealer's cards
                list_cards_dealer.append(name_card)
                # Append list of dealer's val cards
                list_val_cards_dealer.append(val_card)
            n += 1
        print "List cards for player %r " % list_cards_player
        print
        print "First card for dealer %r" % list_cards_dealer[0]

        print
        if list_val_cards_dealer[0] == 11:
            print "Insurance?"
            # The amount bet in this case is not amount double anymore, NEEDS FIXING
            self.take_insurance(amount_bet, list_val_cards_dealer)
        elif list_val_cards_dealer[0] == 10 or list_val_cards_dealer == 11:
            print "Surrender!"
            # Call Surrender method
            self.surrender(amount_bet)

        else:
            self.bust(amount_bet, list_val_cards_player, list_val_cards_dealer, list_cards_player, list_cards_dealer)

        return [n, list_cards_dealer, list_cards_player, list_val_cards_dealer, list_val_cards_player]

    def distribute_1card(self):
        global list_val_cards_player
        num = new_deck.pop(0)
        # Get the name of the new card
        cards.get_name_card(num)
        # Get the value of the new card
        deck.get_val_card(3, name_card)
        # Append list of player's cards
        list_cards_player.append(name_card)
        # Append list of player's val cards
        list_val_cards_player.append(val_card)
        print "List cards for player %r " % list_cards_player
        # print "Values of player's cards %r" % list_val_cards_player
        return list_val_cards_player

    def get_total_val_cards(self, lst):
        # print "This is the get total val cards method\nYour list is %r" % lst
        global total_val_card
        total_val_card = 0
        for num in lst:
            total_val_card += num
        return total_val_card

    def take_insurance(self, amount_bet, list_val_cards_dealer):
        while True:
            print "The insurance would be half of the amount you bet!"
            print
            try:
                answer_insurance = raw_input("Do you want to take an insurance?\n")
                if answer_insurance in player2.positive_answer:
                    amount_insurance = amount_bet / 2.0
                    print u"Your insurance is \u00a3 %r" % amount_insurance
                    print
                    # Check if the dealer has Blackjack
                    self.check_blackjack('Dealer', list_val_cards_dealer, list_val_cards_player,
                                         amount_insurance, amount_bet)
                    break
                    # return insurance, amount_insurance, list_val_cards_dealer
                elif answer_insurance in player2.negative_answer:
                    print
                    self.stand(amount_bet, list_val_cards_player, list_val_cards_dealer)
                    break
                    # return insurance, amount_insurance, list_val_cards_dealer
            except ValueError:
                print "You can only answer yes or no!"
                continue
            finally:
                pass
            # ---------------------THIS METHOD NEEDS TO BE TESTED!!!------------

    def check_blackjack2(self, name, list_val_cards_dealer, list_val_cards_player, amount_insurance, amount_bet):
        global name_player
        total_val_cards_dealer = self.get_total_val_cards(list_val_cards_dealer)
        total_val_cards_player = self.get_total_val_cards(list_val_cards_player)
        print

        if total_val_cards_dealer == 21 and total_val_cards_player == 21:
            print "%s and %s have both a blackjack!!" % (name, name_player)
            self.win_insurance(amount_insurance)
            self.push()
        elif total_val_cards_dealer == 21 and total_val_cards_player != 21:
            print "%s has a blackjack!" % name
            self.win_insurance(amount_insurance)
            print u"You have lost the amount you bet, \u00a3 %.1f" % amount_bet
            self.restart_game()
        elif total_val_cards_dealer != 21 and total_val_cards_player == 21:
            print "You have blackjack!"
            print u"You have won \u003a %.1f " % (amount_bet + (1.0 / 3.0) * amount_bet)
            self.restart_game()
        else:
            self.stand(amount_bet, list_val_cards_player, list_val_cards_dealer)

    def win_insurance(self, amount_insurance):
        print u"You have won\u003a %1.f from your insurance bet!" % (amount_insurance * 2)
        print

    def check_blackjack(self, name, list_val_cards_dealer, list_val_cards_player,
                        amount_insurance, amount_bet):
        # global total_val_card

        # print "Amount bet is %.1f" % amount_bet
        # total_val_card = 0
        # for num in list_val_cards_dealer:
        #     total_val_card += num
        global player
        global name_player
        global list_cards_player
        global list_cards_dealer
        total_val_cards_dealer = self.get_total_val_cards(list_val_cards_dealer)
        total_val_cards_player = self.get_total_val_cards(list_val_cards_player)
        print
        # if amount_bet == '' or amount_insurance == '':
        #     self.check_blackjack_only(total_val_cards_dealer,total_val_cards_player, amount_bet, name_player)
        # else:
        #     self.check_blackjack_insurance(total_val_cards_dealer,total_val_cards_player,amount_insurance,amount_bet)
        if total_val_cards_dealer == 21:
            print "%s has a Blackjack!" % name
            print u"You have won \u00a3 %.1f from your insurance bet" % (amount_insurance * 2.0)
            print "We are now comparing the cards.."
            print
            # Calculate total val cards for player and dealer
            if total_val_cards_player == 21:
                print "%s has also blackjack!" % name_player
                print "No money will be exchanged!"
                # Start the game at the step where we add the amount bet
                # player.set_amount_bet(total_amount_game)
                # player.set_total_amount_game()
                # player.reset_total_amount_game(amount_bet, total_amount_game)

                # THESE ARGUMENTS HAVE NOT BEEN DEFINED!!
            else:
                # Compare val cards
                self.compare_val_cards(total_val_cards_player, total_val_cards_dealer, amount_bet)
            # Discard the cards
            self.discard_cards(list_cards_player, list_cards_dealer)

        else:
            print "%s has no Blackjack!" % name
            print u"You have lost your insurance, \u00a3 %.1f" % amount_insurance
            print "The game will carry on with your hand!"
            print
            # CALL STAND/HIT METHODS -------------------------------------------------
            self.stand(amount_bet, list_val_cards_player, list_val_cards_dealer)

    # -----------TO BE CONTINUED-----------------------
    def check_blackjack_only(self, total_val_cards_dealer, total_val_cards_player, amount_bet, name_player):
        global amount_game
        if total_val_cards_dealer == 21:
            print "Dealer has Blackjack!"
            print
            if total_val_cards_player == 21:
                print "%s has also Bjackjack!\nNo money is exchanged!" % name_player
            else:
                amount_lost = amount_bet +(1.0/3.0) * amount_bet
                print u"You has lost \u00a3 %.1f" % amount_lost
                amount_game = amount_game - amount_lost
        # DISCARD THE CARDS
        # DISTRIBUTE 4 NEW CARDS
        elif total_val_cards_player == 21:
            amount_won = amount_bet +(1.0/3.0) * amount_bet
            print u"%s has Blackjack!\nYou win \u00a3 %.1f" % (name_player, amount_won)
            amount_game = amount_game + amount_won
        # DISCARD THE CARDS
        # DISTRIBUTE 4 NEW CARDS

    def discard_cards(self, list_cards_player, list_cards_dealer):
        global player
        global list_cards_discarded
        global amount_game_left
        global rounds
        rounds += 1
        list_cards_discarded = [list_cards_player.pop(0) for index in range(len(list_cards_player))]
        list_cards_discarded.extend(list_cards_dealer.pop(0) for index in range(len(list_cards_dealer)))
        print "List cards discarded: %r" % list_cards_discarded
        Round2()
        round2.continue_game()
        # THIS METHOD NEEDS TO BE FIXED!!
        # player.set_amount_bet(amount_game_left)


    def prt_test(self):
        print "This is the prt test method in Dealer class"

    def compare_val_cards(self, total_val_cards_player, total_val_cards_dealer, amount):
        # print "List val cards player is %r" % total_val_cards_player
        # print "List val cards dealer is %r" % total_val_cards_dealer
        if total_val_cards_player < total_val_cards_dealer:
            print u"You have lost the amount you bet, \u00a3 %.1f!" % amount
            print "Total value cards dealer is %d" % total_val_cards_dealer
            print "Total value cards player is %d" % total_val_cards_player
            print
            self.restart_game()
        elif total_val_cards_dealer < total_val_cards_player:
            print "Total value cards dealer is %d" % total_val_cards_dealer
            print "Total value cards player is %d" % total_val_cards_player
            print
            print u"You win the amount you bet \u00a3 %.1f!" % amount
            if total_val_cards_player == 21:
                print "You have a Blackjack!"
                amount_blackjack = amount + (amount / 2)
                print u"You have won \u00a3 %.1f!" % amount_blackjack
            print
            self.restart_game()
        elif total_val_cards_player == total_val_cards_dealer:
            self.push()

    def push(self):
        print "We have a push!\nNo money will be exchanged!"
        print
        self.restart_game()

    def restart_game(self):
        print "The game will is restarting.."
        print
        Player()

    def reset_amount_bet(self, total_amount_game):
        global player
        player.set_amount_bet(total_amount_game)

    def stand(self, amount_bet, list_val_cards_player, list_val_cards_dealer):
        while True:
            try:
                print "Stand?"
                print "This would be the end of the game, cards's value will be compared"
                answer_stand = raw_input("Do you want to Stand?\n")
                if answer_stand in player2.positive_answer:
                    # Calculate total value of the cards
                    self.get_total_val_cards(list_val_cards_player)
                    print
                    total_val_cards_player = total_val_card

                    self.get_total_val_cards(list_val_cards_dealer)
                    total_val_cards_dealer = total_val_card
                    print
                    print "Total val cards' player is %d" % total_val_cards_player
                    print "Total val cards' dealer is %d" % total_val_cards_dealer

                    # Compare total values of the cards
                    if total_val_cards_dealer < total_val_cards_player:
                        print u"You have won the amount you bet, \u00a3 %d" % amount_bet
                        self.restart_game()
                        break
                    elif total_val_cards_dealer == total_val_cards_player:
                        self.push()
                        print
                        self.restart_game()
                        break
                    else:
                        print u"You have lost the amount you bet, \u00a3 %d" % amount_bet
                        self.restart_game()
                        break
                elif answer_stand in player2.negative_answer:
                    # print "You have decided not to Stand.\nGood luck!"
                    print
                    self.hit(list_val_cards_player, list_val_cards_dealer)
                    break
            except ValueError:
                print "You can only choose between Yes and No!"
                continue
            finally:
                print

    def hit(self, list_val_cards_player, list_val_cards_dealer):
        # global positive_answer
        # global negative_answer
        # global amount_double
        while True:
            try:
                answer_hit = raw_input("Do you want to HIT?\nYou will get an extra card!\n")
                if answer_hit in player2.positive_answer:
                    # Distribute one extra card
                    self.distribute_1card()
                    print
                    print list_val_cards_player
                    self.bust(amount_bet, list_val_cards_player, list_val_cards_dealer, list_cards_player, list_cards_dealer)
                    break
                    return list_val_cards_player
                elif answer_hit in player2.negative_answer:
                    print "You replied no for HIT\n" \
                          "We will deal with this later!"
                    self.stand(amount_bet, list_val_cards_player, list_val_cards_dealer)
                    print
                    # self.prt_test()
                    # self.stand(list_val_cards_player,list_val_cards_dealer)
                    break
                    # Call STAND method
            except ValueError:
                print "This is the HIT choice, you can only choose between yes or no!"
                continue
            finally:
                pass

    def bust(self, amount_bet, list_val_cards_player, list_val_cards_dealer, list_cards_player, list_cards_dealer):
        global amount_game_left
        print "This is the Bust method\nWe are checking the cards..."
        # print u"We have now the amount game left: \u00a3 %.1f" % amount_game_left
        # global amount_bet
        global player
        # Get total value for the player's cards
        # cards.get_name_card(list_cards_player)
        self.get_total_val_cards(list_val_cards_player)
        total_val_cards_player = total_val_card
        # print "Total value cards for player is %d" % total_val_cards_player
        print

        self.get_total_val_cards(list_val_cards_dealer)
        total_val_cards_dealer = total_val_card
        # print "Total value cards for dealer is %r" % total_val_cards_dealer

        if total_val_cards_dealer > 21:
            print "BUST! dealer has more than 21!"
            print u"Player wins \u00a3 %d" % amount_bet
            print "List cards player: %r" % list_cards_player
            print "List cards dealer: %r" % list_cards_dealer
            self.discard_cards(list_cards_player, list_cards_dealer)
        elif total_val_cards_player > 21:
            print "BUST! player has more than 21!"
            print "List cards player: %r" % list_cards_player
            print "List cards dealer: %r" % list_cards_dealer
            print u"Player loses \u00a3 %d" % amount_bet
            print
            self.discard_cards(list_cards_player, list_cards_dealer)
        else:
            print "None of the hands are higher than 21!"
            print
            self.stand(amount_bet, list_val_cards_player, list_val_cards_dealer)

    def surrender(self, amount_bet):
        global list_cards_discarded
        global list_cards_player
        global list_cards_dealer
        global player
        global amount_game
        list_cards_discarded = []
        while True:
            try:
                answer_surrender = raw_input("Do you want to surrender?\n")
                if answer_surrender in player2.positive_answer:
                    # list_cards_discarded.extend(list_cards_player + list_cards_dealer)
                    # print "List of discarded cards is %r" % list_cards_discarded
                    amount_lost = ((1.0 / 2.0) * amount_bet)
                    print u"You have lost half of the amount you bet, \u00a3 %.1f" % amount_lost
                    amount_bet_left = amount_lost
                    print u"You can keep \u00a3 %.1f" % amount_bet_left
                    amount_game = amount_game + amount_bet_left
                    print
                    self.discard_cards(list_cards_player, list_cards_dealer)
                    break
                elif answer_surrender in player2.negative_answer:
                    print "Good luck!"
                    print
                    self.hit(list_val_cards_player, list_val_cards_dealer)
                    break
            except ValueError:
                print "You can only  choose between Yes and No!"
                continue
            finally:
                pass


class Round2(object):
    global amount_game
    global new_deck


    def __init__(self):
        pass

    def continue_game(self):
        # global amount_game

        while True:
            try:
                answer = raw_input("Do you still want to play?\n")
                if answer in player2.positive_answer:
                    # print "The game will re-start soon. We will deal with this soon!"
                    self.summary_game(amount_game, new_deck)
                    break
                elif answer in player2.negative_answer:
                    print "Shame!\nCome back whenever you like!"
                    break
            except ValueError:
                print "You can only answer Yes or No!"
                continue
            finally:
                pass

    def summary_game(self, amount_game, new_deck):
        print u"You have \u00a3 %d left!" % amount_game
        print "Deck is %r" % new_deck
        # Set the amount bet




global player
global deck
global dealer
global cards
player2 = Player2()
round2 = Round2()
colour = Colour()
deck = Deck()
cards = Cards()
dealer = Dealer()
player = Player()


# global name_card

    
    
    
