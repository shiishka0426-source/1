using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication1
{
    class MyArr
    {
        // Координаты точки в трехмерном пространстве
        public int x, y, z;

        public MyArr(int x = 0, int y = 0, int z = 0)
        {
            this.x = x;
            this.y = y;
            this.z = z;
        }


        // Перегружаем бинарный оператор +
        public static MyArr operator +(MyArr obj1, MyArr obj2)
        {
            MyArr arr = new MyArr();
            arr.x = obj1.x + obj2.x;
            arr.y = obj1.y + obj2.y;
            arr.z = obj1.z + obj2.z;
            return arr;
        }

        // Перегружаем бинарный оператор - 
        public static MyArr operator -(MyArr obj1, MyArr obj2)
        {
            MyArr arr = new MyArr();
            arr.x = obj1.x - obj2.x;
            arr.y = obj1.y - obj2.y;
            arr.z = obj1.z - obj2.z;
            return arr;
        }

        // Перегружаем бинарный оператор *
        public static MyArr operator *(MyArr obj1, MyArr obj2)
        {
            MyArr arr = new MyArr();
            arr.x = obj1.x * obj2.x;
            arr.y = obj1.y * obj2.y;
            arr.z = obj1.z * obj2.z;
            return arr;

        }

        // Перегружаем бинарный оператор /
        public static MyArr operator /(MyArr obj1, MyArr obj2)
        {
            if (obj2.x == 0  obj2.y == 0  obj2.z == 0)
                throw new DivideByZeroException("Деление на ноль запрещено");
            MyArr arr = new MyArr();
            arr.x = obj1.x / obj2.x;
            arr.y = obj1.y / obj2.y;
            arr.z = obj1.z / obj2.z;
            return arr;
        }

        // Перегружаем бинарный оператор %
        public static MyArr operator %(MyArr obj1, MyArr obj2)
        {
            if (obj2.x == 0  obj2.y == 0  obj2.z == 0)
                throw new DivideByZeroException("Деление на ноль при взятии остатка");
            MyArr arr = new MyArr();
            arr.x = obj1.x % obj2.x;
            arr.y = obj1.y % obj2.y;
            arr.z = obj1.z % obj2.z;
            return arr;
        }

        // Унарные операторы
        public static MyArr operator ++(MyArr obj)
        {
            return new MyArr(obj.x + 1, obj.y + 1, obj.z + 1);
        }

        public static MyArr operator --(MyArr obj)
        {
            return new MyArr(obj.x - 1, obj.y - 1, obj.z - 1);
        }



        // Операторы сравнения - попарная перегрузка == и !=
        public static bool operator ==(MyArr obj1, MyArr obj2)
        {
            if (ReferenceEquals(obj1, obj2)) return true;
            if (obj1 is null || obj2 is null) return false;
            return obj1.x == obj2.x && obj1.y == obj2.y && obj1.z == obj2.z;
        }

        public static bool operator !=(MyArr obj1, MyArr obj2)
        {
            return !(obj1 == obj2);
        }




        // Перегружаем операторы true/false
        public static bool operator true(MyArr obj)
        {
            return obj.x != 0  obj.y != 0  obj.z != 0;
        }

        public static bool operator false(MyArr obj)
        {
            return obj.x == 0 && obj.y == 0 && obj.z == 0;
        }

        // Перегружаем логический оператор <
        public static bool operator <(MyArr obj1, MyArr obj2)
        {
            if ((obj1.x < obj2.x)  (obj1.y < obj2.y)  (obj1.z < obj2.z))
                return true;
            return false;
        }

        // Обязательно нужно перегрузить логический оператор >
        public static bool operator >(MyArr obj1, MyArr obj2)
        {
            if ((obj1.x > obj2.x)  (obj1.y > obj2.y)  (obj1.z > obj2.z))
                return true;
            return false;
        }

        // Перегружаем логический оператор <=
        public static bool operator <=(MyArr obj1, MyArr obj2)
        {
            if ((obj1.x <= obj2.x)  (obj1.y <= obj2.y)  (obj1.z <= obj2.z))
                return true;
            return false;
        }
        // Обязательно нужно перегрузить логический оператор >=
        public static bool operator >=(MyArr obj1, MyArr obj2)
        {
            if ((obj1.x >= obj2.x)  (obj1.y >= obj2.y)  (obj1.z >= obj2.z))
                return true;
            return false;
        }

        // Логические операторы (битовые)
        public static MyArr operator &(MyArr obj1, MyArr obj2)
        {
            if (((obj1.x > 0) && (obj1.y > 0) && (obj1.z > 0))
                & ((obj2.x > 0) && (obj2.y > 0) && (obj2.z > 0)))
                return obj1;
            return new MyArr(1, 1, 1);
        }

        public static MyArr operator |(MyArr obj1, MyArr obj2)
        {
            if (((obj1.x > 0)  (obj1.y > 0)  (obj1.z > 0))
                | ((obj2.x > 0)  (obj2.y > 0)  (obj2.z > 0)))
                return obj1;
            return new MyArr(1, 1, 1);
        }

        // Переопределяем методы для правильной работы
        public override bool Equals(object obj)
        {
            return obj is MyArr arr && this == arr;
        }

        public override int GetHashCode()
        {
            return HashCode.Combine(x, y, z);
        }

        public override string ToString()
        {
            return $"({x}, {y}, {z})";
        }
    }

    // Отдельный класс с перегрузкой true/false
    class BoolArray
    {
        private bool[] values;

        public BoolArray(int size)
        {
            values = new bool[size];
        }

        public bool this[int index]
        {
            get => values[index];
            set => values[index] = value;
        }

        // Перегрузка операторов true/false
        public static bool operator true(BoolArray arr)
        {
            foreach (bool value in arr.values)
            {
                if (value) return true;
            }
            return false;
        }

        public static bool operator false(BoolArray arr)
        {
            foreach (bool value in arr.values)
            {
                if (value) return false;
            }
            return true;
        }

        public int Length => values.Length;
    }

    class Program
    {
        static void Main(string[] args)
        {
            MyArr Point1 = new MyArr(1, 12, -4);
            MyArr Point2 = new MyArr(0, -3, 18);

            Console.WriteLine("Координаты первой точки: " + Point1);
            Console.WriteLine("Координаты второй точки: " + Point2 + "\n");

            // Тестирование всех операторов
            MyArr Point3 = Point1 + Point2;
            Console.WriteLine("Point1 + Point2 = " + Point3);

            Point3 = Point1 - Point2;
            Console.WriteLine("Point1 - Point2 = " + Point3);

            Point3 = Point1 * Point2;
            Console.WriteLine("Point1 * Point2 = " + Point3);

            try
            {
                Point3 = Point1 / new MyArr(1, 1, 1);
                Console.WriteLine("Point1 / Point2 = " + Point3);
            }
            catch (DivideByZeroException e)
            {
                Console.WriteLine(e.Message);
            }

            try
            {
                Point3 = Point1 % new MyArr(2, 2, 2);
                Console.WriteLine("Point1 % Point2 = " + Point3);
            }
            catch (DivideByZeroException e)
            {
                Console.WriteLine(e.Message);
            }

            // Унарные операторы
            Point3 = new MyArr(5, 5, 5);
            Console.WriteLine("Исходный temp: " + Point3);

            Point3++;
            Console.WriteLine("temp++: " + Point3);

            ++Point3;
            Console.WriteLine("++temp: " + Point3);

            Point3--;
            Console.WriteLine("temp--: " + Point3);
            // Операторы сравнения
            Console.WriteLine("Попарная перегрузка == и !=");
            Console.WriteLine("Point1 == Point2: " + (Point1 == Point2));
            Console.WriteLine("Point1 != Point2: " + (Point1 != Point2));
            Console.WriteLine("Point1 < Point2: " + (Point1 < Point2));
            Console.WriteLine("Point1 > Point2: " + (Point1 > Point2));
            Console.WriteLine("Point1 <= Point2: " + (Point1 <= Point2));
            Console.WriteLine("Point1 >= Point2: " + (Point1 >= Point2));

            // Тестирование операторов true/false для MyArr
            Console.WriteLine("\nТестирование операторов true/false");
            MyArr zeroPoint = new MyArr(0, 0, 0);
            MyArr nonZeroPoint = new MyArr(1, 0, 0);

            if (zeroPoint)
            {
                Console.WriteLine("Считается true (есть ненулевые координаты)");
            }
            else
            {
                Console.WriteLine("Считается false(есть нулевые координаты)");
            }

            if (nonZeroPoint)
            {
                Console.WriteLine("Считается true (есть ненулевые координаты)");
            }
            else
            {
                Console.WriteLine("Считается false (естьнулевые координаты)");
            }

            // Тестирование отдельного класса с перегрузкой true/false
            Console.WriteLine("\nТестирование класса BoolArray:");
            BoolArray boolArr = new BoolArray(3);
            boolArr[0] = false;
            boolArr[1] = false;
            boolArr[2] = false;

            if (boolArr)
                Console.WriteLine("В массиве ЕСТЬ true значения");
            else
                Console.WriteLine("В массиве НЕТ true значений");

            boolArr[1] = true;

            if (boolArr)
                Console.WriteLine("В массиве ЕСТЬ true значения");
            else
                Console.WriteLine("В массиве НЕТ true значений");
            Console.ReadLine();
        }
    }
}
