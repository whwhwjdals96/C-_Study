# value type, reference type
## Test
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

### Windbg
CsStudy.Program.Main(System.String[])
    PARAMETERS:
        args (0x000000a4505fec80) = 0x000001b280002d38
    LOCALS:
        0x000000a4505fec58 = 0x000001b280002d78
