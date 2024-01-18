# Terminal-and-Bash---Lucky-Duck-Casino-


As the security analyst at Lucky Duck Casino, I successfully completed the assignment to investigate the suspicious activities leading to significant losses on the roulette tables. The largest losses occurred on March 10, 12, and 15, prompting a focused analysis of the player and dealer involved.

**Step 1: Investigation Preparation**

In my web lab virtual machine, I navigated to the HOME directory and set up the necessary directories for the investigation using the specified commands. I created the Lucky_Duck_Investigations directory, which included subdirectories for Player Analysis, Dealer Analysis, and Player-Dealer Correlation. Additionally, I generated empty notes files under each subdirectory.

**Step 2: Gathering Evidence**

I used the wget command to obtain evidence files related to dealer schedules and player wins/losses during the week of March 10. The evidence files were organized into subdirectories named Dealer_Schedules_0310 and Roulette_Player_WinLoss_0310. I moved schedules for March 10, 12, and 15 into the Dealer_Analysis directory and player data for the same dates into the Player_Analysis directory.

**Step 3: Correlating the Evidence**

In the Player_Analysis directory, I employed grep to isolate losses on March 10, 12, and 15 and saved the results in the Roulette_Losses.txt file. I examined the file to identify the times and players associated with the losses and recorded these findings in the Notes_Player_Analysis.txt file.

Moving to the Dealer_Analysis directory, I previewed the dealer schedules and created scripts to extract relevant information about roulette dealers working during the identified loss times. The results were appended to the Dealers_working_during_losses.txt file. I analyzed this file and documented my findings in the Notes_Dealer_Analysis.txt file.

In the Player_Dealer_Correlation directory, I summarized my findings on the player and dealer believed to be colluding, providing specific reasons for this conclusion.

**Step 4: Scripting Your Tasks**

To facilitate future analyses, I developed a shell script named roulette_dealer_finder_by_time.sh in the Dealer_Analysis directory. This script accepts two arguments - date and time - to identify the roulette dealer on duty at a specified time.

The completion of this assignment equips Lucky Duck Casino with the tools and information needed to address the collusion issue and prevent further losses.
