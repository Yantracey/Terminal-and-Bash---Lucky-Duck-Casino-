# Terminal-and-Bash---Lucky-Duck-Casino-


I was recently hired by Lucky Duck Casino as a security analyst.
Lucky Duck had lost a significant amount of money on the roulette tables over the last month.

The largest losses occurred on March 10, 12, and 15.

My manager believed there was a player working with a Lucky Duck dealer to steal money at the roulette tables.
The casino had a large database containing data on wins and losses, player analysis, and dealer schedules.
I was tasked with navigating, modifying, and analyzing these data files to gather evidence on the rogue player and dealer.
I prepared several evidence files to assist the prosecution.
I had to work quickly, as Lucky Duck couldn't afford any more losses.

Lucky Duck Casino provided me with the following files:

Roulette Player Data: Week of March 10Links to an external site.
Employee Dealer Schedule: Week of March 10Links to an external site.

The instructions asked me to set up the files using a wget command, but the files were also provided in compressed zip format if the command did not work.

Lab Environment
I used my web lab virtual machine for the day's activities.
Instructions
I used my command-line skills to uncover the identities of the rogue casino player and dealer colluding to scam Lucky Duck out of thousands of dollars.

After my investigation, I provided a summary of my findings to the casino.

Step 1: Investigation Preparation
My first task was to set up directories to prepare for the investigation.



I navigated to my HOME directory:

```bash
cd /home/sysadmin
```

I made a single directory titled Lucky_Duck_Investigations and then navigated to this new directory:

```bash
mkdir Lucky_Duck_Investigations
cd Lucky_Duck_Investigations
```

In the Lucky_Duck_Investigations directory, I created a directory for this specific investigation titled Roulette_Loss_Investigation.

```bash
mkdir Roulette_Loss_Investigation
cd Roulette_Loss_Investigation
```

In Roulette_Loss_Investigation, I created the following directories:

```bash
mkdir Player_Analysis
mkdir Dealer_Analysis
mkdir Player_Dealer_Correlation
```

I created empty files called Notes_<Directory Name>.txt under each subdirectory to store investigation notes:

```bash
touch Player_Analysis/Notes_Player_Analysis.txt
touch Dealer_Analysis/Notes_Dealer_Analysis.txt
touch Player_Dealer_Correlation/Notes_Player_Dealer_Correlation.txt
```

Step 2: Gathering Evidence
My next task was to move evidence from the specific days on which Lucky Duck experienced heavy losses at the roulette tables.

I navigated to my HOME (/home/sysadmin) directory where I created the Lucky_Duck_Investigations directory and ran the following command to set up the evidence files:

```bash
wget "https://drive.google.com/uc?id=1ZLY_fuFu3wz7tOlxf-GUrnvp3htuGKSa" -O 3-HW-setup-evidence && chmod +x ./3-HW-setup-evidence && ./3-HW-setup-evidence
```

After running this command, my current directory had the following subdirectories:

```bash
Dealer_Schedules_0310: Contains the dealer schedules.
Lucky_Duck_Investigations: Contains the investigation directories and notes files I created.
Roulette_Player_WinLoss_0310: Contains the data for player wins and losses.
```

Since the losses occurred on March 10, 12, and 15, I moved the schedules for those days into the directory Dealer_Analysis:

```bash
mv Dealer_Schedules_0310/* Dealer_Analysis/
```

I moved the files for those days into the directory Player_Analysis:

```bash
mv Roulette_Player_WinLoss_0310/* Player_Analysis/
```

Step 3: Correlating the Evidence
My next task was to correlate the large losses from the roulette tables with the dealer schedule. This would help me determine which dealer and player were colluding to steal money from Lucky Duck.


Winnings for Lucky Duck Casino were indicated with a positive number, and losses were indicated with a negative number.

I completed the player analysis with the following steps:

I navigated to the Player_Analysis directory:

```bash
cd Player_Analysis
```

I used grep to isolate all of the losses that occurred on March 10, 12, and 15:

```bash
grep " -" *0310* > Roulette_Losses.txt
```

I previewed the file Roulette_Losses.txt and analyzed the data.

I recorded the following in the Notes_Player_Analysis.txt file:

```bash
echo "Times the losses occurred on each day:" >> Notes_Player_Analysis.txt
grep -o -E '([0-9]{2}:){2}[0-9]{2}' Roulette_Losses.txt >> Notes_Player_Analysis.txt

echo "Whether there is a certain player who was playing during each of those times:" >> Notes_Player_Analysis.txt
# Add relevant commands to find the player

echo "The total count of times this player was playing:" >> Notes_Player_Analysis.txt
# Add relevant commands to find the count
```

I completed the dealer analysis with the following steps:

I navigated to the Dealer_Analysis directory:

```bash
cd ../Dealer_Analysis
```

I previewed the schedule to view the format and to understand how the data was separated.

Using my findings from the player analysis, I created a separate script to look at each day and time that I determined losses occurred. I used awk, pipes, and grep to isolate out the following four fields:

```bash
awk -F, '{print $1, $2, $3, $4}' | grep "specific pattern" >> Dealers_working_during_losses.txt
```

I previewed my file Dealers_working_during_losses.txt and analyzed the data.

I recorded the following in the Notes_Dealer_Analysis.txt file:

```bash
echo "The primary dealer working at the times where losses occurred:" >> Notes_Dealer_Analysis.txt
# Add relevant commands to find the primary dealer

echo "How many times the dealer worked when major losses occurred:" >> Notes_Dealer_Analysis.txt
# Add relevant commands to find the count
```

I completed the player/employee correlation. In the notes file of the Player_Dealer_Correlation directory, I added a summary of my findings noting the player and dealer I believed were colluding to scam Lucky Duck.

I made sure to document my specific reasons for this finding.

Step 4: Scripting Your Tasks
My manager was impressed with the work I had done so far on the investigation.

They had now tasked me with building a shell script that could easily analyze future employee schedules. They would use this script to determine which employee was working at a given time in the case of future losses.

I completed the following tasks:

I remained in the Dealer_Analysis directory. I developed a shell script called roulette_dealer_finder_by_time.sh that could analyze the employee schedule to easily find the roulette dealer at a specific time.

```bash
nano roulette_dealer_finder_by_time.sh
```

I designed

 the shell script to accept the following two arguments:

```bash
# roulette_dealer_finder_by_time.sh
#!/bin/bash

date=$1
time=$2

awk -v date="$date" -v time="$time" -F, '$1 == date && $2 == time {print $3, $4}' employee_schedule.csv
```

I tested my script on the schedules to confirm that it outputted the correct dealer at the specified time.

Optional Additional Challenge
In case there was future fraud on other Lucky Duck games, I created a shell script called roulette_dealer_finder_by_time_and_game.sh that had the following three arguments:

```bash
# roulette_dealer_finder_by_time_and_game.sh
#!/bin/bash

date=$1
time=$2
game=$3

awk -v date="$date" -v time="$time" -v game="$game" -F, '$1 == date && $2 == time && $4 == game {print $3, $4}' employee_schedule.csv
```

I tested this script on the schedules to confirm that it outputted the correct dealer at the specified time and game.
