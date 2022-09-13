## Boxing/Unboxing
Boxing은 값 형식을 object 형식 또는 이 값 형식에서 구현된 임의의 인터페이스 형식으로 변환하는 프로세스입니다. 
(출처 : [ms](https://docs.microsoft.com/ko-kr/dotnet/csharp/programming-guide/types/boxing-and-unboxing))

## Test Code1
```
namespace CsStudy
{
    class Program
    {
        private static void Main(string[] args)
        {
            int value1 = 10;
            object obj1=value1;
            value1 = 5;


            Console.ReadLine();
        }
    }
}
```
위의 코드와 같이 int에서 object로 변환할 때 (object)를 적지 않고 암시적으로 변환 할 수 있다.
boxing을 하면 힙에 개체 인스턴스를 생성하고 값을 새 개체에 복사.
```
CsStudy.Program.Main(System.String[])
    PARAMETERS:
        args (0x0000004dda7feb40) = 0x000001e920d92d38
    LOCALS:
        0x0000004dda7feb1c = 0x0000000000000005 (**int, 5**)
        0x0000004dda7feb10 = 0x000001e920d92d50 (**object, 포인터**)

0000004dda7fed28 00007ffe16c56893 [GCFrame: 0000004dda7fed28]

0:000> !DumpObj /d 000001e920d92d50
Name:        System.Int32
MethodTable: 00007ffe13cb85a0
EEClass:     00007ffe13e26078
Size:        24(0x18) bytes
File:        C:\Windows\Microsoft.Net\assembly\GAC_64\mscorlib\v4.0_4.0.0.0__b77a5c561934e089\mscorlib.dll
Fields:
              MT    Field   Offset                 Type VT     Attr            Value Name
00007ffe13cb85a0  40005a2        8         System.Int32  1 instance               10 m_value  (**boxing된 값, 10**)

```
위와 같이 boxing은 새 개체를 생성한 것이기 때문에 기존int값을 5로 바꿔도 10이 저장되어 있다.
