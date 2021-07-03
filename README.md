# Overview of Election Audit: 
- The Board of Elections had asked us to audit the congressional election totals to determine the total number of votes, total votes per candidate, percentage of votes won for each candidate, total votes by county, percentage of each county's vote and finally the winning candiate. We were provided a large dataset and tasked with developing the code to quickly and easily validate the results, which will give the public confidence in the winner. 

    - In order to produce the results, we utilzed below software: 
        - Data Source: election_results.csv
        - Software: Python 3.6.1, Visual Studio Code, 1.38.1

# Election-Audit Results:
- By utilizing the software program, Python, we were able to extract the total votes cast in the local Congressional Election to be 369,711 using the below code. 

![image](https://user-images.githubusercontent.com/84824391/124353983-4eb30380-dbcf-11eb-96b4-18636024789e.png)
    
```
#1. Initialize a total vote counter,
total_votes = 0
#Print each row in the CSV file
    for row in file_reader:

        #2. add the total vote count.
        total_votes +=1
#Print the final vote count to the terminal
        election_results = (
            f"\nElection Results\n"
            f"------------------------\n"
            f"Total Votes: {total_votes:,}\n"
            f"------------------------\n")
        print(election_results, end="")
        #Save the final vote count to the text file
        txt_file.write(election_results)
```

- We obtained a breakdown of the number of votes and the percentage of total votes for each county in the precinct using the below code.

![image](https://user-images.githubusercontent.com/84824391/124354145-2546a780-dbd0-11eb-8d29-672f60d9e6e9.png)

```              
        for county_name in county_votes:
            #6b: Retrieve the county vote count.
            total_county_votes = county_votes.get(county_name)
            #6c: Calculate the percentage of votes for the county.
            county_vote_percentage = float(total_county_votes) / float(total_votes) * 100    

            #6d: Print the county results to the terminal.
            county_results = (
                f"{county_name}: {county_vote_percentage:.1f}% ({total_county_votes:,})\n")
            
            print(county_results, end="")
        
            #6e: Save the county votes to a text file.
            
            txt_file.write(county_results)
```

- We determined that Denver County had the largest number of votes at 306,055, which was 82.8% of the total vote.
 
![image](https://user-images.githubusercontent.com/84824391/124354153-2e377900-dbd0-11eb-878f-531f077bfdac.png)

```   
   #6f: Write an if statement to determine the winning county and get its vote count.
            if (total_county_votes > largest_county_votes):
                largest_county = county_name
                largest_county_votes = total_county_votes
        #7: Print the county with the largest turnout to the terminal.
        largest_county_summary = (
            f"----------------------\n"
            f"Largest County Turnout: {largest_county}\n"
            #f"Largest County Turnout: {largest_county_votes}\n"
            f"----------------------\n")
        
        #8: Save the county with the largest turnout to a text file.
        txt_file.write(largest_county_summary)
```

- We also provided a breakdown of the number of votes and the percentage of the total votes each candidate received.

![image](https://user-images.githubusercontent.com/84824391/124354158-38597780-dbd0-11eb-9d87-8091e50dc0c4.png)

```
#Save the final candidate vote count to the text file.
        for candidate_name in candidate_votes:

            #Retrieve vote count and percentage
            votes = candidate_votes.get(candidate_name)
            vote_percentage = float(votes) / float(total_votes) * 100
            candidate_results = (
                f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

            #Print each candidate's voter count and percentage to the
            #terminal.
            print(candidate_results)
            #Save the candidate results to our text file.
            txt_file.write(candidate_results)
```

- And the winner of the election was Dinaa DeGette, with 272,892 votes, which was 73.8% of the vote.
 
![image](https://user-images.githubusercontent.com/84824391/124354165-43140c80-dbd0-11eb-95a5-e97f2fe7a8d5.png)

```
#Determine winning vote count, winning percentage, and candidate.
            if (votes > winning_count) and (vote_percentage > winning_percentage):
                winning_count = votes
                winning_candidate = candidate_name
                winning_percentage = vote_percentage

        #Print the winning candidate (to terminal)
        winning_candidate_summary = (
            f"-------------------------\n"
            f"Winner: {winning_candidate}\n"
            f"Winning Vote Count: {winning_count:,}\n"
            f"Winning Percentage: {winning_percentage:.1f}%\n"
            f"-------------------------\n")
        print(winning_candidate_summary)

        #Save the winning candidate's name to the text file
        txt_file.write(winning_candidate_summary)
```

# Election-Audit Summary: 

- In summary, we were able to develop a code to quickly determine the results of this election. We believe that the underlying structure of this code can easily be adapted to future congressional elections, but also other elections. While this code was focused on the "county level", we can easily replace the names and queries to reflect "state", "city" or other political boundaries based upon how the data is collected. We can also apply this code to elections that may involved "Propositions" or non-person elections by replacing the structure related to the winning candidate's name. 
