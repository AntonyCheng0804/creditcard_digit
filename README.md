# creditcard_digit
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
int main()
{
	//initialize variable for format "XXXX" to save data
	int a, b, c, d;//for calculate
	printf("Enter partial card number: ");
	scanf("%4d%4d%4d%4d", &a, &b, &c, &d);//allow user to imput the partial card number
	int i, j, m = 0;
	int S[17];//initialize array length for saving 16 digit
	int T[] = { a,b,c,d };//Another array for saving four pair of digit "XXXX"
	for (i = 0; i != 4; i++)
	{
		for (j = 1; j != 5; j++)//Get each digit from input 
		{
			S[j + m] = T[i] % 10;//Use array to save the value of each digit 
			T[i] /= 10;
			//printf("S[%d]=%d and a = %d\n", j+m, S[j+m], T[i]);//used to check
		}
		m += 4;//To maintain the element of array wont overlapped
	}
	//Rearrange the order of element in the array
	int tmp;
	for (i = 0; i != 12; i += 4)
	{
		tmp = 0;
		tmp = S[i + 4];
		S[i + 4] = S[i + 1];
		S[i + 1] = tmp;
		tmp = 0;
		tmp = S[i + 3];
		S[i + 3] = S[i + 2];
		S[i + 2] = tmp;
	}
	//swapping the 13th and 16th digit (Group D)
	tmp = 0;
	tmp = S[16];
	S[16] = S[13];
	S[13] = tmp;
	//swapping the 14th and 15th digit (Group D)
	tmp = 0;
	tmp = S[15];
	S[15] = S[14];
	S[14] = tmp;
	if (S[13] == 0)//testing the final four digit have wrong position or not
	{
		S[13] = S[14];
		S[14] = S[15];
		S[15] = S[16];
		S[16] = 0;
	}
	int W[17];
	//calculation
	for (i = 1; i != 17; i++)
	{
		if (i % 2 == 1) //when odd then true
			W[i] = S[i] * 2;//Double the odd-positional digits
		else
			W[i] = S[i];
	}
	for (i = 1; i != 17; i++)
	{
		if (W[i] > 9)//when double digit is greater than 9 then do
		{
			W[i] = (W[i] % 10) + (W[i] / 10 % 10);//replace it by sum of digits
		}
	}
	int sum = 0;//initialize the sum of 15 digit
	for (i = 1; i != 17; i++)
	{
		sum += W[i];
	}
	//printf("sum is %d\n", sum);//use for test

	//Find the check digit 
	S[16] = sum * 9 % 10;
	//output
	printf("Full card number is ");
	int x = 0;
	for (i = 0; i != 4; i++)
	{
	for (j = 1; j != 5; j++)
		{
			printf("%d", S[j + x]);
		}
	x += 4;
	printf(" ");
    }
	return 0;
}
	
	
	
	
	

	
	
	
	
	
	
	
	
	
	
	
	
	
	
	


	
	
