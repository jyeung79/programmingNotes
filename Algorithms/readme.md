# Programming Interview Practice

What should I do? Should I follow the Scenario 3: Term Project (1 month) or Scenario 4: Algorithms Class (4 months)

Let's just do Scenario 4 (4 month) because I have no interest of spending more than 1 hour or (2 pomods) on coding problems. Perhaps as this habit develops but for now just follow Scenario 4.

Should I join the telegram group for programming interview help or such? Yes. Absolutely.

## Questions to Do

| CO | Cl | C2 | C3 | C4 |
|----|----|----|----|----|
| [] 5.1 | 5.7 | 5.8 | 5.3, 5.11 | 5.9 |
| 6.1, 6.6 | 6.11, 6.17 | 6.2, 6.16 | 6.5, 6.8 | 6.3, 6.9, 6.14 |
| 7.1 | 7.2, 7.4 | 7.5, 7.6 | 7.7, 7.8 | 7.9, 7.11 |
| 8.1 | 8.2, 8.3 | 8.4, 8.7 | 8.10 | 8.11 |
| 9.1 | 9.7 | 9.2, 9.8 | 9.3, 9.9 | 9.4 |
| 10.1 | 10.4 | 10.2, 10.12 | 10.11 | 10.13, 10.16 |
| 11.1 | 11.4 | 11.3 | 11.5 | 11.7 |
| 12.1 | 12.4, 12.8 | 12.3, 12.9 | 12.5, 12.10 | 12.6, 12.7 |
| 13.2 | 13.6, 13.3 | 13.1, 13.6 | 13.4, 13.7 | 13.10 |
| 14.1 | 14.2 | 14.4 | 14.6, 14.9 | 14.7 |
| 15.1 | 15.2, 15.3 | 15.4, 15.8 | 15.5, 15.9 | 15.7, 15.10 |
| 16.1 | 16.2 | 16.3 | 16.4, 16.9 | 16.6, 16.10 |
| 17.1 | 17.2 | 17.3, 17.6 | 17.5, 17.7 | 17.12 |
| 18.4 | 18.6 | 18.5, 18.7 | 18.8 | 25.34 |
| 19.1 | 19.7 | 19.2 | 19.3 | 19.9 |
| 20.3 | 20.6 | 20.8 | 20.9 | 21.9 |
| 21.13 | 21.15 | 21.16 | 21.1 | 21.2 |

- **C0, C1** - Hackathon (3 days) 
- **C2** - Finals cram (7 days) 3-4 hours
- **C3** - Term Project (1 month) 1.5-2.5 hours
- **C4** - Algorithms Class (4 months) 1 hour


### Ch. 5 Questions

#### 5.9 - Check if the Decimal Integer is a palindrome

Write a program that takes in an integer and determines if that integer as a decimal string is a palindrome.

> ie) 12321, 0, 7, 121, 7487847 are palindromes

> ie) 14731, -4, 478574 are not palindromes

The bruteforce method would be to convert it as a string and then looping through the entire string to match the pairwise digits.

However, a better method to do it in ```O(logn)``` time complexity is to have two pointers starting at the beginning and the end of the string. Then checking if the pair of digits are equal. If not, return false and if yes, increment the start pointer and decrement the end pointer. Continue iterating through the sting until your start pointer index > end pointer index.

I see this above problem solving technique in other past questions as well.


#### 6.3 - MULTIPLY TWO ARBITRARY-PRECISION INTEGERS

