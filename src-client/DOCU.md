# Game & Class Structure Documentation

## Game

- 2 to 4 Players.
- 4 Towers.
- 1 Deck.

```javascript
{
    'players': [
        Player
    ],
    'towers': [
        [Card],
        [Card],
        [Card],
        [Card]
    ],
    'deck': [Card]
}
```

### Player

Participant of the game. User or oponnent.

```javascript
{
    'name': String,
    'stocks': [
        [Card],
        [Card],
        [Card],
        [Card]
    ],
    'stack': [Card],
    'hand': [Card]
}
```

#### Stock

Four 'trash piles'. The players add one card to any of their four stocks at the end of their turn. It can be used to stack the towers during their turn. Only the latest 'trashed' card can be used before the card underneath it per stock.

```javascript
[Card]
```

#### Stack

Players' personal stack of cards they have to deplete to win.

```javascript
[Card]
```

#### Hand

Maximum of five cards held by a player.

```javascript
[Card]
```

### Tower

Stacks of cards that can only be stacked in ascending order. Clears when rank 12 is reached. A SkipBo card may be placed on top of any rank.

```javascript
[Card]
```

### Deck

Shuffled stack of cards which the players draw from at the start of their turns.

```javascript
[Card]
```

### Card

Rank ranged from numbers 1 to 12. Rank 0 represents a SkipBo card.

Colors:

- 1-4: `#437cff`
- 5-8: `#3aac30`
- 9-12: `#c52b42`
- SkipBo (0): `#ffa343`

```javascript
{
    'rank': Number,
    'isFaceUp': Boolean
}
```