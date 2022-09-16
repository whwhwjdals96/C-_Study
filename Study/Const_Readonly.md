# Const, Readonly?
## Test Code1
```
    class Program
    {
        static void Main(string[] args)
        {

            Console.WriteLine();
        }
    }

    class Test
    {
        static readonly int R = 100; //런타임 상수 : 메서드 내부 선언 불가
        const int C = 200; //컴파일타임 상수: 메서드 내부에서 선언 가능

        public void ShowResult()
        {
            if(GetNumber() == C)
            {
                Console.WriteLine("Compile Time");
            }
            if(GetNumber() == R)
            {
                Console.WriteLine("Run Time");
            }
        }

        int GetNumber()
        {
            return 100;
        }
    }
```
## Const  
'''
.field private static literal int32 C = int32(0x000000C8)(ildasm으로 확인)
'''
1. 암시적으로 정적이다.  
Test Code1에서 Const선언할 때 static을 따로 적지 않았지만 static으로 선언되어 있는 것을 확인 할 수있다.
