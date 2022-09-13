# Struct 메모리 테스트
## Test Code1
```
    class Program
    {
        private static void Main(string[] args)
        {
            ClassTest test = new ClassTest(9, "class");
            // 디버거 접속대기
            Console.ReadLine();

            test.Display();
        }
    }

    class ClassTest
    {
        int value1;
        string testString;
        structTest structtest;

        public ClassTest(int i, string s)
        {
            value1 = i;
            testString = s;
            structtest = new structTest(31, "hello struct");
        }
        public void Display()
        {
            Console.WriteLine(value1);
            Console.WriteLine(testString);
            Console.WriteLine(structtest);
        }
    }

    struct structTest
    {
        int a;
        string b;

        public structTest(int i,string s)
        {
            a = i;
            b = s;
        }
    }
```
## Windbg
```
0:000> !do 0x00000188ad8e2d78
Name:        CsStudy.ClassTest
MethodTable: 00007ffaf1775c08
EEClass:     00007ffaf17725c0
Size:        48(0x30) bytes
File:        C:\Users\whwhw\source\repos\CsStudy\CsStudy\bin\x64\Debug\CsStudy.exe
Fields:
              MT    Field   Offset                 Type VT     Attr            Value Name
00007ffb4dfc85a0  4000001       10         System.Int32  1 instance                9 value1
00007ffb4dfc59c0  4000002        8        System.String  0 instance 00000188ad8e2d50 testString
00007ffaf1775b68  4000003       18   CsStudy.structTest  1 instance 00000188ad8e2d90 structtest  (**Struct Value에 시작 주소 값이 들어있다**)

0:000> !DumpVC /d 00007ffaf1775b68 00000188ad8e2d90
Name:        CsStudy.structTest
MethodTable: 00007ffaf1775b68
EEClass:     00007ffaf1772638
Size:        32(0x20) bytes
File:        C:\Users\whwhw\source\repos\CsStudy\CsStudy\bin\x64\Debug\CsStudy.exe
Fields:
              MT    Field   Offset                 Type VT     Attr            Value Name
00007ffb4dfc85a0  4000004        8         System.Int32  1 instance               31 a (**int의 값**)
00007ffb4dfc59c0  4000005        0        System.String  0 instance 00000188ad8e2da8 b (**string 포인터**)

0:000> dq 0x00000188ad8e2d78+18 (**객체 주소 + Offset**)
00000188`ad8e2d90  00000188`ad8e2da8 00000000`0000001f  (**struct의 string 포인터와 int 값이 들어있다.**)
```

## 
Struct는 Struct의 포인터를 반환하는 것이 아닌 메모리 상에 값을 가지고있다. Struct의 필드에 ref type이 있으면 해당 포인터를 저장한다.
