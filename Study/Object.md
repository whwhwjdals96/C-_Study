## Object ??
.NET 클래스 계층 구조의 모든 클래스를 지원하며 파생 클래스에 하위 수준 서비스를 제공합니다. 이는 모든 .NET 클래스의 궁극적인 기본 클래스이며 형식 계층 구조의 루트입니다. (출처 : MS)  
```
    class ClassTest
    {
        int value1;
        public ClassTest(int i)
        {
            value1 = i;
        }

        public override bool Equals(object obj)
        {
            return base.Equals(obj);
        }
        public override int GetHashCode()
        {
            return base.GetHashCode();
        }
        public override string ToString()
        {
            return base.ToString();
        }

        public void Display()
        {
            Console.WriteLine(value1);
        }
    }
```
상속을 따로 해주지 않았지만 함수 override가 가능하다. => 암시적 상속  
.NET 형식 시스템의 모든 형식은 Object 또는 여기에서 파생된 형식에서 암시적으로 상속합니다.  
|형식 범주|다음에서 암시적으로 상속|
|---|---|
|class|Object|
|struct|ValueType, Object|
|enum|Enum, ValueType, Object|
|delegate|MulticastDelgate, Delegate, Object|  (출처 : MS)
