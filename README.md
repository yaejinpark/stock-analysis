# Stock Analysis - Berkeley DA
Yae Jin Park
Module 2: VBA of Wall Street

## Project Overview
For the stock analysis project, I was able to demonstrate basic coding knowledge in VBA by refactoring a mock stock analysis code. The purpose of this project was to use for loops, logical operators, and basic VBA formatting in order to produce a set of calculations without having to manually sort through thousands of rows with repeating calculations. 

There are only twelve different stocks for this dataset, but thousands of rows of data that show their volumes, starting prices and ending prices on different days. Though possible, it is extremely time-consuming and inefficient even using the filter function provided in Excel for each stock (or tickers). Though the numbers themselves don't form a pattern, the dataset itself has a pattern in that each row contains the same type of data: stock name, date, prices, etc., all 8 columns in total. Using this knowledge to my advantage, I was able to obtain the following results as the final outcome. 

## Results
![VBA_Challenge_2017](/resources/VBA_Challenge_2017.png)
Return rates of the stocks in 2017


![VBA_Challenge_2018](/resources/VBA_Challenge_2018.png)
Return rates of the stocks in 2018

### Code
Please refer to the VBA code in Module1 through Developer Mode in VBA_Challenge.xlsm.

In the given template of unfinished VBA code, the first step I took was to define three arrays, each for ticker volumes, starting prices, and ending prices. Since there are twelve tickers, I gave all three arrays lengths of 12. Since ticker volumes are the first values to be calculated, I initially set all of the elements in the array as 0 for initialization. This was done by setting a for loop that ran from steps 0 to 11 (same as the indices in the volume array) and having each array element starting from tickerVolume[0] to equal to 0. Each element in the tickerVolume array represents the sum of volume of each ticker.

Next, with the given ticker arrays, I went through every single row except for the top row in the given datasheets (2017 and 2018) and performed some calculations. The key to getting an accurate result was to use the ticker index to establish a connection between the tickers array and the ticker data arrays. Starting from the first ticker in the ticker array, I checked that the row I'm in had the same ticker name as I did in the ticker array at the current ticker index. If the names in both matched, I added the volume to one of the ticker volume array element. 

Then, my code looks for the starting price of the same ticker by checking if the current row is the first for the ticker the code is currently iterating. If the previous row's ticker name does not match the current row's ticker name, then that indicates that the current row is the first row for the current ticker, indicating that the current row contains the starting price of the ticker. I set this starting price as an element in the starting price array.

Following a similar logic, I check if the current row is the last row for the current ticker by checking the next row's ticker name. If the ticker names don't match for the two rows, then the current row the code is iterating through contains the ending price. I set this current row's price as the ending price by setting it as an element in the ending price array. Since there is no more data to extract from the current ticker, I increment the ticker index so that I can repeat the above process (minus the defining and initialization) for all rows in the datasheets.

## Summary
### Advantages and Disadvantages of Refactoring Code
Since the outcome of this code is supposed to demonstrate the same results as the one I wrote throughout the module exercises, this assignment can be defined as a refactoring task. 

The advantage of refactoring the code is that I know what results I want, so I can write the code in a more efficient, cleaner way. For example, the module exercises code used a nested for loop, which is frowned upon when there are big amounts of data to iterate through and the Big-O is O(n^2), where n is the number of samples in the data. If I had one million more lines of rows of data, the nested for loop would be significantly slower than the one I wrote for this challenge. Let's say that the for loop integers, i and j, each run from 0 to a million. While i (the outer for loop) is on 0, it will have to wait until j (the inner for loop) to reach a million. Then repeat this a million times, and I would be finally done with the for loops. For the challenge's solution, I used separate for loops but not nested ones, resulting in an O(n+m), which is more efficient. 

Though it's difficult to think of a disadvantage of refactoring code in general (I was always taught to do so after initially making a block of code work), I can see that refactoring made the code more complex in a way. Compared to the module exercises version, I had more variable names I had to keep track of (array names, ticker index, etc.) and was getting errors when testing my code due to unintentional misuses of them. I was getting confused which variable names meant what and had to spend 90% of my debugging time finding out if I was storing the right data in the right array. The code became more efficient for the machine to run, but not necessarily for the humans to read and comprehend. Some people might say that this isn't a disadvantage, but if someone else who has no idea what this code should do had to work with this code, would they be able to fully understand it? Comments are supposed to help with this issue, but simple code would be easier to understand than reading a verbose comment of what the code does.

I guess that the phrase "You can't have the cake and eat it too" applies to coding too - I can't always have a block of simple, easy-to-read code lines that are also the most efficient and optimized at the same time. The key is to find the right balance between code efficiency and easier reading and do my best to leave comments in critical spots (with complicated logic) and more.

### Advantages and Disadvantages of the Original VBA Script
As mentioned in the Advantages and Disadvantages of Refactoring Code, the advantage for the original VBA script was that it was easy to read and keep track of. Instead of storing the ticker volume, starting price, and ending price in arrays, the code inserted the values in the cells right away, getting rid of the need to keep track of which array contains what. It was also easier to test with the original script because I didn't run into any errors related to arrays (e.g. index out of bounds, happened because the for loop that contained the code that populated the array had faulty logic and kept trying to iterate through the array more than the array's length), making debugging a whole lot easier. The disadvantage is the inefficient nested for loop, again, mentioned in the section above. I was fortunate to have a dataset of only a couple thousand rows, or else, I'm not sure if my computer would have been able to run properly.

### Advantages and Disadvantages of the Refactored VBA Script
Again, efficiency is the big advantage for the refactored script (please see Advantage two sections above this section). If I had to run this code on a similar but a much larger dataset, I'm still confident that my computer wouldn't blow up from too much caluclation. The disadvantage is that I had to juggle with three similarly named arrays and debugging became very confusing. There was also a point where the for loop that should populate all three arrays only populated the first element in all three arrays, even if the range of the for loop was set correctly from 2 to number of rows in the datasheet. This was particularly hard to debug because this meant that the logic was correct for the first iteration, but for some reason was faulty in the second, which didn't make any sense because I can't change the code while it's executing. Again, I found the fault was that I used the wrong variable names in logical operators, which brings me back to my point that refactoring made my code more complex in a way.
