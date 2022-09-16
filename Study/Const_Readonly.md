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
### Const  
```
.field private static literal int32 C = int32(0x000000C8) // ildasm으로 확인
```
**암시적으로 정적이다. 또한 값이 들어있다.**  
Test Code1에서 Const선언할 때 static을 따로 적지 않았지만 static으로 선언되어 있는 것을 확인 할 수있다.
### Readonly
```
.field private static initonly int32 R // ildasm으로 확인
```
**값이 아직 들어있지 않다.**
```
### Test Code1의 ShowResult메서드 부분을 확인해보자
.method public hidebysig instance void  ShowResult() cil managed
{
  // 코드 크기       47 (0x2f)
  .maxstack  8
  IL_0000:  ldarg.0
  IL_0001:  call       instance int32 ConsoleApp2.Test::GetNumber()
  IL_0006:  ldc.i4     0xc8 // 값이 들어있다.
  IL_000b:  bne.un.s   IL_0017
  IL_000d:  ldstr      "Compile Time"
  IL_0012:  call       void [System.Console]System.Console::WriteLine(string)
  IL_0017:  ldarg.0
  IL_0018:  call       instance int32 ConsoleApp2.Test::GetNumber()
  IL_001d:  ldsfld     int32 ConsoleApp2.Test::R // 참조로 컴파일되어있다.
  IL_0022:  bne.un.s   IL_002e
  IL_0024:  ldstr      "Run Time"
  IL_0029:  call       void [System.Console]System.Console::WriteLine(string)
  IL_002e:  ret
} // end of method Test::ShowResult
```
### Const  
값과 GetNumber()를 비교한다.  
### Readonly  
직접적인 값이 아닌 참조로 GetNumber()와 비교한다.
## 
즉 Const는 컴파일을 하면 대체된다. 반면에 Readonly는 런타임이 되기 전까진 값을 평가하지 않는다.
