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
---
Const: 암시적으로 정적이다, 컴파일타임에 값이 평가, 매서드 내부 선언 가능, 선언시에만 초기화
'''

'''
