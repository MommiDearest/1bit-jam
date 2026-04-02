# Card Game Minimal Game Loop

## Goal

3-round game, 2 phases per round

---

## Game Phases

### Phase 1: Card Match Game

- Cards displayed face down on screen (8/10/12 depending on the round)
- Player gets 3 peeks
- Each peek: click any two cards > they show face up > flip back down
- Players can use their peeks (counted by tokens) cards shuffle, players try to track them
- Players can skip their peeks and pick 2 cards as their final cards
- Those selected 2 cards get added to the players deck

### Phase 2: Card Grid Game

- 3x3 grid, 9 cells
- Player flips coin, if they go first they can place up to 5 cards, if they go second they only get 4
- Player/Enemy place cards, the cell behind them fills in with their color (white for player/black for enemy)
- Enemy placement random (no ai)
- Cards placed face down
- After grid is full: 
  - Each card compares ATK on a touching side vs the neighbor's DEF on that side
  - ATK > DEF: that card flips to your color
  - No cascade:  resolve only immediate neighbors, once 
- Count cards 5 or more = WIN

---

## Additional Features

### Deck Build and Steal

- Peeks tracked by tokens
- Enemy's best card is in the pool 
- Finding it 'steals' it from enemy deck

### Grid Game 

- Tokens used to redo coin flip, or to flip enemy card during game 
- Enemy placement ai, focuses on placing strong cards in good positions
- Cascade: cards will flip neighbors, and neighbors can flip other cards in turn

### Round Progression

| Round | Cards Face-Down | Peeks |
|-------|----------------|-------|
| 1     | 8              | 3     |
| 2     | 10             | 3     |
| 3     | 12             | 3     |

- Win all 3 rounds > game complete screen
- Lose a round > game over screen
- Minimum card set needed: 6 player cards + 3 enemy "best" cards (one per round) = 9 unique cards

---
  
## Milestones

### Card Data & Rendering
- [ ] Define card data make tool to create cards easily
- [ ] Render a single card face-up and face-down
- [ ] Load full starting deck and enemy hands from a data file

### Phase 1 Playable
- [ ] Lay N cards face-down on screen
- [ ] Peek mechanic: click 2 > reveal > flip back (3 peeks total)
- [ ] Shuffle after all peeks used
- [ ] Player selects 2 cards > build player hand

### Phase 2 Playable
- [ ] Render 3x3 grid
- [ ] Alternate placement: player clicks to place, enemy places randomly
- [ ] Resolve ATK vs DEF on touching sides > flip color (no cascade)
- [ ] Count score, show WIN or LOSE

### Full Round Loop
- [ ] Phase 1 > Phase 2 > result > card steal / card loss
- [ ] Deck state persists across rounds
- [ ] Round counter increments, face-down card count scales correctly

### 3-Round Game Complete
- [ ] 3 rounds run in sequence
- [ ] Game complete screen on winning all 3
- [ ] Game over screen triggers correctly
