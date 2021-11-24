# Nhóm gồm 3 thành viên:
- Lê Trần Lâm Bình - 19020226
- Nguyễn Duy Đường - 19020266
- Hoàng Văn Đô - 19020251

## Link
* Link Github Project: https://github.com/abishekaditya/DesignPatterns
* Link mẫu chuẩn: https://refactoring.guru/design-patterns/java
# Creational Patterns
## 1. Abstract Factory
- Là một mẫu thiết kế sáng tạo cho phép bạn tạo ra các họ các đối tượng liên quan mà không cần chỉ định các lớp cụ thể của chúng.
- Code: [Abstract Factory](https://github.com/abishekaditya/DesignPatterns/tree/master/FactoryPattern/Abstract%20Factory)
- Ở đây, cung cấp một interface cho việc tạo lập các đối tượng (có liên hệ với nhau) mà không cần qui định lớp khi hay xác định lớp cụ thể (concrete) tạo mỗi đối tượng, 2 class được khai báo theo mẫu chuẩn.
```
internal class ChicagoIngredientsFactory : IIngredientsFactory
internal class NyIngredientsFactory : IIngredientsFactory
```

## 2. Factory Method
- Là một mẫu thiết kế sáng tạo cung cấp một giao diện để tạo các đối tượng trong lớp cha, nhưng cho phép các lớp con thay đổi loại đối tượng sẽ được tạo.
- Code: [Factory Method](https://github.com/abishekaditya/DesignPatterns/tree/master/FactoryPattern/Factory%20Method)
- 
```
abstract class PizzaFactory
    {
        public Pizza Order(string type) {}
        protected abstract Pizza Create(string type);
    }
class ChicagoPizzaFactory : PizzaFactory
    {
        protected override Pizza Create(string type) {}
    }
class NyPizzaFactory : PizzaFactory
    {
        protected override Pizza Create(string type) {}
    }
```
## 3. Builder
- Builder là một mẫu thiết kế sáng tạo cho phép bạn xây dựng các đối tượng phức tạp theo từng bước. Mẫu cho phép bạn tạo ra các kiểu và hình ảnh đại diện khác nhau của một đối tượng bằng cách sử dụng cùng một mã xây dựng.
- Khởi tạo interface IBuilder:
```
public interface IBuilder
    {
        void AddIngredients();
        void AddShape();
        void AddSize();
        void Reset();
        Hamburger Build();
    }
```
- Các lớp MyHamburgerBuilder, WifesHamburgerBuilder kế thừa các thuộc tính trong lớp IBuilder. Tách tiến trình xây dựng 1 đối tượng phức tạp sao cho một tiến trình tạo được các biểu diễn khác nhau 
=> Builder Design Pattern
## 4. Prototype Pattern
- Prototype là một mẫu thiết kế sáng tạo cho phép bạn sao chép các đối tượng hiện có mà không làm cho mã của bạn phụ thuộc vào các lớp của chúng.
- Code: [Prototype Pattern](https://github.com/abishekaditya/DesignPatterns/tree/master/PrototypePattern)
- Khởi tạo `interface IFigure : ICloneable` dùng làm đối tượng mẫu để quy định các loại đối tượng của lớp Circle và Rectangle, hai lớp đó kế thừa lớp IFigure. Tất cả các lớp sau tuân theo cùng một interface, cung cấp một phương thức clone().
```
interface IFigure : ICloneable
    {}
class Circle : IFigure
    {
        public object Clone()
        {
            return new Circle(_radius);
        }
    }
class Rectangle : IFigure
    {
        public object Clone()
        {
            return new Rectangle(_width, _height);
        }
    }
 ```
 - Giống với mẫu chuẩn trong [Prototype Pattern](https://refactoring.guru/design-patterns/prototype)
 
 ## 5. Singleton
 - Singleton cho phép đảm bảo rằng một lớp chỉ có một thể hiện, đồng thời cung cấp một điểm truy cập toàn cục cho thể hiện này.
 - Class `ChocolateBoiler` được khởi tạo là `internal partial class ChocolateBoiler`, bên trong là phương thức khởi tạo tĩnh và phương thức khởi tạo private.
 ```
 internal partial class ChocolateBoiler
    {
        private static readonly Lazy<ChocolateBoiler> _singleton = new Lazy<ChocolateBoiler>(() => new ChocolateBoiler());

        public static ChocolateBoiler GetInstance() => _singleton.Value;

        private Status _boiler;

        private ChocolateBoiler()
        {
            Console.WriteLine("Starting");
            _boiler = Status.Empty;
        }

        public void Fill() {}

        public void Drain() {}

        public void Boil() {}

        private bool IsEmpty => (_boiler == Status.Empty);

        private bool IsBoiled => (_boiler == Status.Boiled);
    }
 ```
 - Giống với mẫu chuẩn trong [Singleton](https://refactoring.guru/design-patterns/singleton)
 
 # Behavioral Patterns
 ## 1. Chain of Responsibility
 - cho phép chuyển các yêu cầu dọc theo một chuỗi các trình xử lý. Khi nhận được yêu cầu, mỗi trình xử lý sẽ quyết định xử lý yêu cầu hoặc chuyển nó cho trình xử lý tiếp theo trong chuỗi.
 - 
 
