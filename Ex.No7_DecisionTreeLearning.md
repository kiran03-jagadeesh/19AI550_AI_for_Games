### Ex.No: 7 Implementation of Decision Tree Learning 
### REGISTER NUMBER :212221230078
### AIM:
Design a decision tree for following data. 
 Healthy, In Cover, With Ammo -> Attack
Hurt, In Cover, With Ammo -> Attack
Healthy, In Cover, Empty -> Defend
Hurt, In Cover, Empty -> Defend
Hurt, Exposed, With Ammo -> Defend
### Algorithm:
1. Start the program
2. import the necessary packages 
3. Design a training data and test data 
4. Create a decision tree classifier model
5. Output the predictions 
6. Visualize the decision tree
    
### Program:
```
class DecisionTree:
    def __init__(self):
        self.tree = {
            "Healthy": {
                "In Cover": {
                    "With Ammo": "Attack",
                    "Empty": "Defend"
                },
                "Exposed": {
                    "With Ammo": "Defend",
                    "Empty": "Defend"
                }
            },
            "Hurt": {
                "In Cover": {
                    "With Ammo": "Attack",
                    "Empty": "Defend"
                },
                "Exposed": {
                    "With Ammo": "Defend",
                    "Empty": "Defend"
                }
            }
        }

    def decide(self, health, cover, ammo):
        return self.tree[health][cover][ammo]

# Create a decision tree
tree = DecisionTree()

# Test the decision tree
print(tree.decide("Healthy", "In Cover", "With Ammo"))  # Output: Attack
print(tree.decide("Hurt", "In Cover", "With Ammo"))  # Output: Attack
print(tree.decide("Healthy", "In Cover", "Empty"))  # Output: Defend
print(tree.decide("Hurt", "In Cover", "Empty"))  # Output: Defend
print(tree.decide("Hurt", "Exposed", "With Ammo"))  # Output: Defend

# Assign the result to a variable
result = tree.decide("Healthy", "In Cover", "With Ammo")
print(result)  # Output: Attack

# Use the result in a conditional statement
if result == "Attack":
    print("You attack!")
elif result == "Defend":
    print("You defend!")
```

### Output:

![Screenshot 2024-10-04 140300](https://github.com/user-attachments/assets/3f5c1b59-f1f1-4be0-bc44-e251615c00c5)


### Result:
Thus the optimum value of max player was found using minimax search.
