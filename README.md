# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: My first approach was to find all the duplicates from the grid and then look for the twins in the grid. For each twin box, I was trying to remove the match character(character which were present in both peers and twins) from peers.
	
	dups = dict()
    for key, value in values.items():
        if len(value) == 2:
            if value not in dups:
                dups[value] = [key]
            else:
                dups[value].append(key)
    
    twins = dict()
    for key,value in dups.items():
        if len(value) == 2:
            if not key in twins:
                twins[key] = value
            else:
                twins[key].extend(value) 

    for key in twins:
        for box in twins[key]:
            print(peers[box])
            for peer in peers[box]:
                for key_element in list(key):
                    if values[peer] != key and len(values[peer])>=2:
                        assign_value(values, peer, values[peer].replace(key_element, ''))

 But after looking the explaination on http://www.sudokudragon.com/tutorialnakedtwins.htm, I got to know my the fault in my approach.
 So, I changed my approach to remove matching character from either row_units and square units or column_units and square_units as twins will make impact on either row or column but not on both at the same time.

# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: I just create the diagonal units and add it to the unitlist. Units are being to used to create peers list to make sure that numbers are not repeated in any unit.

### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project. 
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Code

* `solution.py` - You'll fill this in as part of your solution.
* `solution_test.py` - Do not modify this. You can test your solution by running `python solution_test.py`.
* `PySudoku.py` - Do not modify this. This is code for visualizing your solution.
* `visualize.py` - Do not modify this. This is code for visualizing your solution.

### Visualizing

To visualize your solution, please only assign values to the values_dict using the ```assign_values``` function provided in solution.py

### Submission
Before submitting your solution to a reviewer, you are required to submit your project to Udacity's Project Assistant, which will provide some initial feedback.  

The setup is simple.  If you have not installed the client tool already, then you may do so with the command `pip install udacity-pa`.  

To submit your code to the project assistant, run `udacity submit` from within the top-level directory of this project.  You will be prompted for a username and password.  If you login using google or facebook, visit [this link](https://project-assistant.udacity.com/auth_tokens/jwt_login for alternate login instructions.

This process will create a zipfile in your top-level directory named sudoku-<id>.zip.  This is the file that you should submit to the Udacity reviews system.

