# credit.c-cs50-
credit.c(CS50)
#include<stdio.h>
#include<cs50.h>
bool isAmex(long long n);
bool isMastercard(long long n);
bool isVisa(long long n);
int length(long long n);
int start2number(long long n,int m);
bool check(long long n,int l);
int add(int m); 
 int main(void)
 {
     long long n;
     do
     {
         printf("number:");
         n=get_long_long();
     }while(n<0);
     if (isAmex(n))
     {
         printf("AMEX\n");
     }
     else if (isMastercard(n))
     {
         printf("MASTERCARD\n");
     }
     else if (isVisa(n))
     {
         printf("VISA\n");
     }
     else printf("INVALID\n");
     return 0;
 }
 bool isAmex(long long n)
 {
     int l=length(n);
     if (l==15)
     {
         if (start2number(n,l)==34||start2number(n,l)==37)
         {
             return check(n,l) ;
         }
         else return false;
     }
     else return false;
     
 }
 bool isMastercard(long long n)
 {
     int l=length(n);
     if (l==16)
     {
         if (start2number(n,l)<=55&&51<=start2number(n,l))
         {
             return check(n,l) ;
         }
         else return false;
     }
     
     else return false;
 }
 bool isVisa(long long n)
 {
     int l=length(n);
     if (l==13||l==16)
     {
         int j=start2number(n,l)/10;
         if (j==4)
         {
            return check(n,l) ;
         }
         else return false;
     }
     else return false;
 }
 int length(long long n)
 {
     int i=0;
     while(n>0)
     {
         n=n/10;
         i++;
     }
     return i;
 }
 int start2number(long long n,int m)
 {
     
     for (int i=0;i<m-2;i++)
     {
         n=n/10;
     }
     
     return n;
 }
 bool check(long long n,int l)
 {
     long long m;
     int sum1=0;
     int sum2=0;
     int sum;
     for (int i=0;i<l;i++)
     {
         m=n;
         for (int j=l-i;j>1;j--)
         {
             m=m/10;
         }
         m=m%10;
         if ((l-i)%2==0)
         {
             sum1=sum1+add(m);
         }
         else
         {
             sum2=sum2+m;
         }
     }
     sum=sum1+sum2;
     if (sum%10==0)
     return true;
     else
     return false;
 }
 int add(int m)
 {
    if(m<5)
    {
        return 2*m;
    }
    else 
    {
        int n=m*2%10;
        return n+1;
    }
 }
