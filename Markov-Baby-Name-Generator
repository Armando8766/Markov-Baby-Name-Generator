import time
from random import randint
print("##################################################################\n###############\tWelcome to Baby Name Generator\t##################\n##################################################################\n")

print("Well, first tell me that do you want the names for a Baby boy or baby girl?\n")
ans = ''
while True:
    ans = input("Please enter 1 for baby boy's names and 2 for baby girl's names...")
    try:
        if ans == '1':
            print("\nBaby boy it is\nOkay, now answer the following questions,\n")
            file = open("namesBoys.txt")
        if ans == '2':
            print("\nBaby girl it is\nOkay, now answer the following questions,\n")
            file = open("namesGirls.txt")
        assert(ans == '1' or ans == '2')
        break
    except:
        print("\nDuuuuuude! only enter 1 or 2...\n")

minimumLetters = 0
while True:
	try:
		minimumLetters = int(input("What should be the MINIMUM number of letters for the name that you are looking for?\n"))
		assert(minimumLetters > 0)
		break
	except:
		print("Duuuuuuude! Enter a number greater than zero")


maximumLetters = 0
while True:
	try:
		maximumLetters = int(input("What should be the MAXIMUM number of letters for the name that you are looking for?\n"))
		assert(maximumLetters > 0)
		break
	except:
		print("Duuuuuude! Enter a number greater than zero")

Markov_order = 0
while True:
    try:
        Markov_order = int(input('You know how Markov models work, right?! Tell me what do you want for Markov order number?\n'))
        assert(Markov_order > 0)
        break
    except:
        print("Dude! Enter a number greater than zero")

count = 0
while True:
    try:
        count = int(input('aaaaaand lastly, How many names would you like to see?\n'))
        assert(count > 0)
        break
    except:
        print("Dude you are killing me! Enter a number greater than zero")

def Markov(Markov_order,file):
    names = []
    #creating a list of names and adding '_' before and after the names
    key = ""
    for i in range(0, Markov_order):
        key = key + "_"
    for name in file:
        names.append(key + name.lower() + key)
    Pattern = {}
    for name in names:
        #finding keys and their letters for each name in the list
        for idx in range(0, len(name) - Markov_order):
            key = name[idx:Markov_order + idx]
            next_Letter = name[idx + Markov_order:idx + Markov_order + 1]
            #Check if the key already exists ib the pattern
            if key in Pattern:
                current = Pattern[key]
                if next_Letter in current:
                    current[next_Letter] += 1
                else:
                    current[next_Letter] = 1
                Pattern[key] = current
            else:
                newLetter = {}
                newLetter[next_Letter] = 1
                Pattern[key] = newLetter
    return Pattern

#getting the keys and corresponding letters
def getLetters(key, arrange):
    letters = arrange[key]
    return letters

#Generating next letter based on the current pattern among letters
def nextLetter(Markov_order,name, arrange):
    letters = getLetters(name[len(name) - Markov_order:len(name)], arrange)
    Characters_list = []
    Characters = list(letters.items())
    for (key, value) in Characters:
        for i in range(0, value):
            Characters_list.append(key)
    # selecting letters randomly based on their probability of occurance in the pattern
    rand_idx = randint(0, len(Characters_list) - 1)
    Letter = Characters_list[rand_idx]
    return Letter



def Markov_BabyNames_Generator():
    print("\nOkay, wait a second,\nBaby names are loading...\n")
    time.sleep(3)
    Pattern = Markov(Markov_order, file)
    i = 0
    # Using a loop for generating the number of names that the user specified at the beginning
    while (i < count):
        #This is for adapting names length to the number selected for order when selecting final names
        name = "_" * Markov_order
        while len(name) < maximumLetters + Markov_order:
            letter = nextLetter(Markov_order,name, Pattern)
            if letter == '_':
                break
            name += letter
        newName = name.replace('\n', '').replace('\r', '')
        if (len(newName[Markov_order:]) > minimumLetters ):
            print ('>>>>',newName[Markov_order:])
            i += 1
Markov_BabyNames_Generator()
