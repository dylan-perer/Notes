## Prime numbers

```c#
using System;

namespace ConsoleApp1
{
    internal class Program
    {
        static void Main(string[] args)
        {
            for(int i = 0; i < 50; i++)
            {
                string x = isPrime(i) ? "is prime" : "not prime";
                Console.WriteLine($"Number {i} {x}");
            }
        }

        private static bool isPrime(int x)
        {
            //positive
            //greater than 1
            //divisable by is self

            if (x == 1 || x <=0)
            {
                return false;
            }
            else
            {
                for (int i = 2; i < 1000; i++)
                {
                    if (x % i==0)
                    {
                        if (i != x)
                        {
                            return false;
                        }
                    } 
                }
                return true;
            }
        }
    }
}

```