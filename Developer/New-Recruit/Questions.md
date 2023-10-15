# Database Challenges

## Question 1

Please see the attached ERD diagram image. The diagram was submitted as a solution to storing employee Cellphone data, voice and sms usage.
Discuss at least one improvement that can be done to the ERD.

I think that one important improvement that can be made to the ERD is breaking down complex attributes, like location(County, City, Suburb...) details, into separate tables. This reduces redundancy, streamlines data maintenance, and enhances data integrity, making the database more organized and reliable.

## Question 2

An analyst has asked you to run a query to see the number of movie tickets per genre that was sold in December last year. The data he needs is spread across two tables.


Table Examples:


[Tickets] (Stores all the movie tickets sold) 


TicketID	| #Seat Number | #MovieID
--- | --- | --- |
10 | 1A | 1
20 | 2B | 2
30 | 4C | 3


[Movies] (Stores all the different Movies)


MovieID	| #Name | #Genre 
--- | --- | --- |
1	| Citizen Kane | Drama
2 | Shutter Island | Mystery
3 | Scarecrow | Comedy


Using a SQL script, retrieve the data the analyst requires.

```sql 
SELECT M."Genre", COUNT(T."TicketID") AS "Tickets Sold" 
FROM "Movies" AS M
LEFT JOIN "Tickets" AS T ON M."MovieID" = T."MovieID"
GROUP BY M."Genre"
ORDER BY "Tickets Sold" DESC;
```

# Back-end Code Challenges
* Only send back the code required for your the challenges

## Question 1

Write a C# method that will take, as input, a string and dependent on the string length prints out the following:
1. If the length is a multiple of 2 your method must print out "Stack"
2. If the length is a multiple of 4 your method must print out "Overflow"
3. If the length is a multiple of 2 and 4 your method must print out "Stack Overflow!"

```csharp
using System;
class CheckingStringLength
{
    static void Main(string[] args)
    {
        while (true) // Loop to continue the game
        {
            Console.WriteLine("Enter a String (word):");
            string input = Console.ReadLine();

            // Check for empty or whitespace input and request valid word
            if (string.IsNullOrWhiteSpace(input))
            {
                Console.WriteLine("Please enter a valid word.");
                continue; 
            }

            // Check for input with spaces (multiple words) and request input again
            if (input.Contains(" "))
            {
                Console.WriteLine("Please enter a word without spaces.");
                continue; 
            }

            DetermineOutput(input);

            // Provide the option to continue (Y) or exit (N)
            Console.WriteLine("Do you want to check another word? (Y/N)");
            string response = Console.ReadLine();

            if (response.Trim().Equals("N", StringComparison.OrdinalIgnoreCase))
            {
                Console.WriteLine("Thanks for playing.");
                break;
            }
        }
    }


    static void DetermineOutput(string input)
    {
        int wordLength = input.Length;

        // Determine the output based on input conditions. If none of the conditions are met, prompt for a different word. 
        if (wordLength % 2 == 0 && wordLength % 4 == 0)
        {
            Console.WriteLine("Stack Overflow!");
        }
        else if (wordLength % 2 == 0)
        {
            Console.WriteLine("Stack");
        }
        else if (wordLength % 4 == 0)
        {
            Console.WriteLine("Overflow");
        }
        else
        {
            Console.WriteLine("None of the conditions were met. Try a different word!");
        }
    }
}
 ```

## Question 2
This task is about code refactoring. Below you are given classes Animal, Horse and Sheep.

You need to refactor Horse and Sheep as you see fit. The goal is to make the classes more maintainable. You should apply any principles or patterns you think are necessary.

Don't make any change to the properties (methods) of the class Animal.

```csharp
    // Not making any changes to the Animal class, as per instructions above.
    public class Animal
    {
        public string Eat()
        {
            return "Yummy";
        }

        public virtual string MakeNoise()
        {
            return "Durrr";
        }
    }

    // Using a concept in OOP (Inheritance).
    class Horse : Animal
    {
        // Overriding the MakeNoise() method to return "Neigh"
        public override string MakeNoise(){
            return "Neigh";
        }
    }

    // Using a concept in OOP (Inheritance).
    class Sheep : Animal
    {
        // Overriding the MakeNoise() method to return "Baaah"
        public override string MakeNoise(){
            return "Baaah";
        }
    }



```
# Front-end Code Challenges

## Question 1
Given the below code snippet, solve the problems that follow:

```html
<div id="firstDiv" class="red-card">
<div id="secondDiv" class="red-card">

<style>
    #secondDiv {
        background: orange;
    }

    div {
        height: 150px;
        width: 150px;
        background: green;
    }

    .red-card {
        background: red;
    }

    .yellow-card {
        background: yellow;
    }
</style>
```

1. What will the colour of both div elements be?

The colour of the first div element (<div id="firstDiv" class="red-card">) will be red and the colour of the second div element (<div id="secondDiv" class="red-card">) will be orange.


2. How would you dynamically target ```firstDiv``` and make it's colour pink? (provide the code snippet)


<!--  I would add a button on the firstDev element, and when the button is clicked the firstDiv element will change from red to pink. Below I've added code which should be in the html file to implement this. -->

    ```html
    <button onclick="changeColor()">Click to change colour to Pink</button>


    <script>
        function changeColor() {
            var firstDiv = document.getElementById("firstDiv");
            if (firstDiv) {
            firstDiv.style.backgroundColor = "pink";
            }
        }
        </script>
    ```

<!-- Alternatively if you'd want the page to load with the firstDev already being pink we can: -->
    ```html

    <div id="firstDiv" class="pink-card">

    <style>
    .pink-card {
        background: pink;
    }
    </style>
        ``

3. How would you dynamically target ```secondDiv``` and add the ```yellow-card``` class to its class list? (provide the code snippet)
<!-- Working on solution -->


## Question 2
Consider the function below:

```javascript
function legal(x) {
    console.log(x);
    var x;
}
```

1. Why will the function be parsed correctly? 

Yes. This js function will be parsed correctly. Even though the variable is declared after the console.log. The var x will be hoisted to the top of the legal() fuction.

2. How could you introduce a stricter syntax to variable/function declaration and avoid this behaviour?

There are two ways in which we can introduce a stricter syntax:

1.Firstly, we can use strict mode ("use strict"). This will result in the function throwing an error (ReferenceError) because the var x has not been declared.

2.We can also change the keyword that is being used. Instead of using var, we can use the keywords - let or const as those keywords are block scoped, so they can only be accessed within the block in which they are declared in.
