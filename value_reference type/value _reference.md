# value type, reference type
## 값 타입과 Collection
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
