# Lab 9 Group 1

## Group members
* Jack McGrath
* Olivia Joe West
* Amos Lou

## Exercise 1
1. The GET method is a method used to retrieve data/information from the API you are requesting. 
If I wanted to create 2 decks then I would use the GET parameter "deck_count=2". The url would look like: https://deckofcardsapi.com/api/deck/new/shuffle/?deck_count=2

2. 
* Shuffle the cards
* Draw a card
* Reshuffle the cards
* Create brand new deck
* Create partial deck
* Create/add to piles
* Shuffle piles
* List cards in piles
* Draw cards from piles

3. https://deckofcardsapi.com/api/deck/new/?jokers_enabled=true

4. 
* Two cards are drawn from the deck. The cards are the King of Hearts and 8 of Clubs.
* ``` let deck = {
    "success": true,
    "cards": [
        {
            "image": "https://deckofcardsapi.com/static/img/KH.png",
            "value": "KING",
            "suit": "HEARTS",
            "code": "KH"
        },
        {
            "image": "https://deckofcardsapi.com/static/img/8C.png",
            "value": "8",
            "suit": "CLUBS",
            "code": "8C"
        }
    ],
    "deck_id":"3p40paa87x90",
    "remaining": 50
}

deckID = deck.deck_id
console.log(deckID) ```
* ``` Enter code here ```

## Exercise 2
``` Enter code here ```
