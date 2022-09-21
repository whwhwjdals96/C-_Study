# 객체 생성 value type, reference type
## Test Code1
    class Program
    {
        private static void Main(string[] args)
        {
            Test test = new Test(9,1.2222,"hello");

            // 디버거 접속대기
            Console.ReadLine();

            test.Display();
        }
    }

    class Test
    {
        int value1;
        double value2;

        string testString;

        public Test(int i, double d, string s)
        {
            value1 = i;
            value2 = d;
            testString = s;
        }
        public void Display()
        {
            Console.WriteLine(value1);
            Console.WriteLine(value2);
            Console.WriteLine(testString);
        }
    }

## Windbg (x64)
 ```
 CsStudy.Program.Main(System.String[]) [C:\Users\whwhw\source\repos\CsStudy\CsStudy\Program.cs @ 16]
    PARAMETERS:
        args (0x000000a4505fec80) = 0x000001b280002d38
    LOCALS:
        0x000000a4505fec58 = 0x000001b280002d78 (**Main()의 test**)

000000a4505fee68 00007ffb50d66893 [GCFrame: 000000a4505fee68] 
0:000> !do 0x000001b280002d78 (**객체 확인**)
Name:        CsStudy.Test
MethodTable: 00007ffaf1785b18
EEClass:     00007ffaf1782578
Size:        40(0x28) bytes
File:        C:\Users\whwhw\source\repos\CsStudy\CsStudy\bin\x64\Debug\CsStudy.exe
Fields:
              MT    Field   Offset                 Type VT     Attr            Value Name
00007ffb4dfc85a0  4000001       18         System.Int32  1 instance                9 value1         (**값이 들어있다.**)
00007ffb4dfcad70  4000002       10        System.Double  1 instance 1.222200 value2                 (**값이 들어있다.**)
00007ffb4dfc59c0  4000003        8        System.String  0 instance 000001b280002d50 testString     (**주소가 들어있다.**)
 ```
### value1(int), value2(double) 주소를 확인해보자
```
0:000> dd 0x000001b280002d78+18                        (**18은 offset**)
000001b2`80002d90  00000009 00000000 00000000 00000000 (**9가 들어가 있는 모습을 확인할 수 있다.**)

0:000> dq 0x000001b280002d78+10                        (**10은 offset**)
000001b2`80002d88  3ff38e21`9652bd3c 00000000`00000009 (**3ff38e21`9652bd3c 확인해보자**)
```

```
var hex = 0x3ff38e219652bd3c;
byte[] bytes = BitConverter.GetBytes(hex);
Console.WriteLine(BitConverter.ToDouble(bytes, 0)); 
//결과 : 1.2222
```

### testString을 확인해보자
```
0:000> !do 000001b280002d50 (**string의 주소확인**)
Name:        System.String
MethodTable: 00007ffb4dfc59c0
EEClass:     00007ffb4dfa2ec0
Size:        36(0x24) bytes
File:        C:\Windows\Microsoft.Net\assembly\GAC_64\mscorlib\v4.0_4.0.0.0__b77a5c561934e089\mscorlib.dll
String:      hello
Fields:
              MT    Field   Offset                 Type VT     Attr            Value Name
00007ffb4dfc85a0  4000283        8         System.Int32  1 instance                5 m_stringLength
00007ffb4dfc6838  4000284        c          System.Char  1 instance               68 m_firstChar
00007ffb4dfc59c0  4000288       e0        System.String  0   shared           static Empty
0:000> db 000001fc22d82d50+c  (**string의 first char의 메모리 확인**)
000001fc`22d82d5c  68 00 65 00 6c 00 6c 00-6f 00 00 00 00 00 00 00  h.e.l.l.o....... (**hello 확인가능**)
 ```
## 값 형식
값 형식은 **System.Object**에서 파생된 **System.ValueType**에서 파생  
값 형식 변수에는 해당 값이 직접 포함  
값 형식 변수에 대한 힙 할당X, 가비지 수진 오버헤드 없음  
값 형식은 **sealed**, 값 형식에서 파생 할 수 없음  
struct(값 형식)는 System.ValueType을 (암시적)상속 받았다 => C#은 하나의 Class만을 상속 받을 수 있다.  
하지만 interface는 상속을 할 수 있다. => interface는 다중 상속이 가능하다. [링크](https://github.com/whwhwjdals96/C-_Study/blob/main/Study/Boxing.md#%EC%B6%94%EA%B0%80)
## 참조 형식
delegate, 배열, interface, class, recode  
개체가 만들어지면 관리되는 힙에 메모리 할당.  
변수는 개체의 위치에 대한 참조만을 가진다.  
배열은 System.Array에서 암시적으로 파생
