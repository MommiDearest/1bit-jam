# Card Game - Game Design Document


## Concept

A single-player card game in two phases per round. Face-down cards are spread on the screen. Somewhere among them are the best cards. Find them, use them in a grid battle, and steal the enemy's best card when you win. Your deck grows stronger as you progress. Three rounds, escalating difficulty.

Theme: What's hiding in there?
Players: 1
Rounds: 3
Win condition: Win all 3 grid battles

---

## Core Loop (Per Round)

```
PHASE 1: 
> Cards are laid face-down on screen
> Player gets limited peeks to find the 2 highest ATK cards
> Player selects 2 cards as their guess
> Found cards (and unfound ones) form the player's battle hand

PHASE 2: 
> 3x3 grid
> Player and enemy alternate placing cards
> After grid is full: flip all cards, resolve battles
> Higher ATK vs neighbor's DEF = flip that card to your color
> Most cards your color = WIN

ON WIN
> Player steals the enemy's best card > added to their deck
> Deck grows stronger for future rounds

ON LOSS
> Enemy takes one of the player's best cards
> Losing your best card early hurts more than later (you have more by then)
```

---

## Phase 1 Rules Detail

- Cards are placed face-down on screen
- Player has 3 peeks. Each peek: click any 2 cards > they show face-up briefly, then flip back down
- After all peeks used (or skipped), cards shuffle once
- Player clicks 2 cards as their final guess - these are their battle cards that are added to the deck
- If both are correct (highest ATK cards) > strong hand going into battle
- If one or none correct > weaker hand, harder battle ahead
- The 2 selected cards + 2 random cards from the pool form the player's 4-card hand

Face-down card count per round (increases difficulty):
| Round | Cards Face-Down | Peeks |
|-------|----------------|-------|
| 1 | 8 | 3 |
| 2 | 10 | 3 |
| 3 | 12 | 3 |

*More cards = harder to remember where the best ones are.*

---

## Phase 2 Rules Detail

- 3x3 grid, 9 cells
- Each card has ATK/DEF values on each of its 4 sides
- Player and enemy alternate placing cards until grid is full (4 cards each + 1 filler) 
- filler card can belong to player or enemy, flip a coin to decide. If you didnt use up your 'peek' tokens before, you can flip again for the cost of 1 token
- Resolve: each card compares its ATK on a touching side vs the neighbor's DEF on that side
  - ATK > DEF: that card flips to your color
  - Cascades: a newly flipped card can flip its own neighbors
- Score: count cards of each color
- 5+ of 9 your color = WIN

Enemy hand: the enemy always plays their best 4 cards for that round. Finding your best cards is what makes the fight fair.

---

## Cards

Cards have 4 sides, each labeled ATK or DEF with a value (1-8).

## Deck Growth (The Meta Loop)

- Win Round 1 > steal E1-D > deck is now 7 cards
- Win Round 2 > steal E2-D > deck is now 8 cards
- Win Round 3 > steal E3-D > deck is now 9 cards

The payoff: the more you win early, the more cards are in the face-down pool in later rounds - which means your best cards are harder to find too, but the rewards are greater. Losing a card to the enemy hurts less the more cards you've accumulated.

---

## Win / Lose States

| State | Trigger | Result |
|-------|---------|--------|
| Round Win | 5+ cards your color | Steal enemy's best card |
| Round Loss | 4 or fewer cards your color | Enemy takes one of your best cards |
| Full Win | Win all 3 rounds | Game complete |
| Deck depleted | Lose too many cards | Game over (stretch goal) |

---

## Scope Notes

Must have:
- Phase 1: face-down cards, peek mechanic, guess selection
- Phase 2: grid placement, flip resolution, color scoring
- Card steal on win / card loss on defeat
- 3 rounds with increasing face-down card count
- unique card design for each 'best' card

Nice to have:
- Card flip and reveal animations
- Enemy "thinking" pause before placement
- Win/loss fanfare

Cut if needed:
- Cascade flips - resolve only immediate neighbors if time is tight
- Enemy AI strategy - random placement is fine
