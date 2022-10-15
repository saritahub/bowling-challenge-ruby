# Plan
User INPUTS rolls
With the user inputs, the program calculates the score

## User stories
As a user
So I can keep count of each roll
I’d like to input the number of pins knocked down

As a user
So I can see my frame score
I’d like to see the sum of the rolls for each frame (harder, maybe show as a breakdown)

As a user
So I can see my overall score
I’d like to see the total score at the end of the tenth frame

### Nouns
Pins (knocked down from each roll)
Score

### Verbs
(Input) roll
Frame score (keep in mind, no bonus for tenth frame)
Overall game score

## How does bowling scoring work?
Bowling game
10 frames in which the player tries to known down the 10 pins
In each frame, the player can roll one or two times (the actual number depends on strikes and spares)
Score of a frame is the number of knocked down pins plus bonuses for strikes and spares
After every game, the 10 pins are reset

## How does Bowling work
### Strikes
Player has a strike if they knock down all 10 pins within the first roll in a frame
Frame ends immediately (as there are no pins left for a second roll)
BONUS for that frame:
Number of pins knocked down by the next two rolls
That would be the next game, unless the player rolls another strike

### Spares
Player has a space if they knock down all 10 pins with the two rolls of a frame
BONUS for that frame:
Number of pins knocked down by the next roll
That is the first roll of next frame (unless the score is 0 for Roll 1, then Roll 2 is the bonus)

### 10th frame
If the player rolls a strike or spare in the 10th frame, they can roll the additional balls for the bonus
If they don’t roll a strike or spare, no additional balls (??)
Cannot roll more than 3 balls in the 10th game
The additional rolls only count for the bonus, not for the regular frame count

10, 10, 10 in the 10th frame gives 30 points (10 points for the regular first strike and 20 points for the bonus).
1, 9, 10 in the 10th frame gives 20 points (10 points for the regular spare and 10 points for the bonus).

### Gutter game
If the player never hits a pin (20 zero scores)

### Perfect game
When a player rolls 12 strikes
10 regular strikes
2 strikes for the bonus in the 10th frame
Score is 300 points



## How does user input work
Score starts as 0
User will input ALL their scores in one go
User input converted in to an array
MVP: Numerical works
Advanced: Numerical with Strikes and Spares as X

pin_count = ‘XX XX XX XX XX XX XX XX XX XXX’
Please put all of the scores with format ‘XX XX XX XX XX XX XX XX XX XXX’
Note: Even if you didn’t get a bonus roll for frame 10, please put ‘0’Score from user input
Convert the string (pin_count) to an array
Then break the arrays down (Maybe an array of arrays, test this out in irb before)
Then add the scores from each frame to another array (overall score)

pin_count_frame_1 = [10, 0] => (10 + 3 + 4) 17 (STRIKE)
pin_count_frame_2 = [3, 4] => (17 + 7)  24
pin_count_frame_3 = [8, 2] => 35 (SPARE)
pin_count_frame_4 = [5, 5] => (35 + 10 + 1) 46 (SPARE)
pin_count_frame_5 = [1, 2] => 49
pin_count_frame_6 = [7, 2] => 58
pin_count_frame_7 = [8, 2] => (58 + 10 + 10) 78 (SPARE)
pin_count_frame_8 = [10, 0] => (78 + 10 + 0 + 5) 93 (STRIKE)
pin_count_frame_9 = [0, 5] => 98
pin_count_frame_10 = [5, 5, 5] => 113 (SPARE, NO BONUS)

Then scores for each frame calculated

Score calculation for a STRIKE (Frame 1 - 9)
If roll 1 = 10, this is a STRIKE
Scoring for strikes reminder
BONUS for that frame:
Number of pins knocked down by the next two rolls
That would be the next game, unless the player rolls another strike

10 pins knocked down plus bonus from the next two rolls

score_frame_1 = 17
Frame 1: 10 + 0 = 10 (sum of that array)
Frame 2 roll 1: 3
Frame 1 roll 2: 4

If pin_count_frame_1[0] == 10 || frames 1..9
frame_score is equal to 10 + next two rolls
frame_score = 10 + the next array roll 1 + the next array roll 2

However, if the next array roll 1 == 10
Then add the next NEXT array’s roll 1 Score calculation for a SPARE (Frame 1 - 9)
If roll 1 + roll 2 = 10, this is a SPARE
Reminder of spare scores

Player has a space if they knock down all 10 pins with the two rolls of a frame
BONUS for that frame:
Number of pins knocked down by the next roll
That is the first roll of next frame (unless the score is 0 for Roll 1, then Roll 2 is the bonus)


pin_count_frame_3 = [8, 2] => 35 (SPARE)
pin_count_frame_4 = [1, 2]

frame_score = 10 + roll 1 of next frame
If roll 1 of next frame is 0, add roll 2 of next frame


TENTH FRAME SCORE CALCULATIONS
If roll 1 + roll 2 >= 10
Then roll 3 exists
If not, then roll 3 = 0

For the sake of simplicity, just add together the total 