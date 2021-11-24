# Nhóm gồm 3 thành viên:
- Lê Trần Lâm Bình - 19020226
- Nguyễn Duy Đường - 19020266
- Hoàng Văn Đô - 19020251

## Link
* Link Github Project: https://github.com/abishekaditya/DesignPatterns
* Link mẫu chuẩn: https://refactoring.guru/design-patterns/java
# 1. Creational Patterns
## 1.1 Abstract Factory
- Là một mẫu thiết kế sáng tạo cho phép bạn tạo ra các họ các đối tượng liên quan mà không cần chỉ định các lớp cụ thể của chúng.
- Code: [Abstract Factory](https://github.com/abishekaditya/DesignPatterns/tree/master/FactoryPattern/Abstract%20Factory)
- Ở đây, cung cấp một interface cho việc tạo lập các đối tượng (có liên hệ với nhau) mà không cần qui định lớp khi hay xác định lớp cụ thể (concrete) tạo mỗi đối tượng, 2 class được khai báo theo mẫu chuẩn.
```
internal class ChicagoIngredientsFactory : IIngredientsFactory
internal class NyIngredientsFactory : IIngredientsFactory
```

## 1.2 Factory Method
- Là một mẫu thiết kế sáng tạo cung cấp một giao diện để tạo các đối tượng trong lớp cha, nhưng cho phép các lớp con thay đổi loại đối tượng sẽ được tạo.
- Code: [Factory Method](https://github.com/abishekaditya/DesignPatterns/tree/master/FactoryPattern/Factory%20Method)
- Lớp tạo khai báo phương thức gốc phải trả về một đối tượng của một lớp sản phẩm. Các lớp con ChicagoPizzaFactory, NyPizzaFactory cung cấp việc triển khai phương thức này.
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
## 1.3 Builder
- Builder là một mẫu thiết kế sáng tạo cho phép bạn xây dựng các đối tượng phức tạp theo từng bước. Mẫu cho phép bạn tạo ra các kiểu và hình ảnh đại diện khác nhau của một đối tượng bằng cách sử dụng cùng một mã xây dựng.
- Code: [Builder](https://github.com/abishekaditya/DesignPatterns/tree/master/BuilderPattern)
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
## 1.4 Prototype Pattern
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
 
 ## 1.5 Singleton
 - Singleton cho phép đảm bảo rằng một lớp chỉ có một thể hiện, đồng thời cung cấp một điểm truy cập toàn cục cho thể hiện này.
 - Code: [Singleton](https://github.com/abishekaditya/DesignPatterns/tree/master/SingletonPattern)
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
 
 # 2. Behavioral Patterns
 ## 2.1 Chain of Responsibility
 - cho phép chuyển các yêu cầu dọc theo một chuỗi các trình xử lý. Khi nhận được yêu cầu, mỗi trình xử lý sẽ quyết định xử lý yêu cầu hoặc chuyển nó cho trình xử lý tiếp theo trong chuỗi.
 - Code: [Chain of Responsibility](https://github.com/abishekaditya/DesignPatterns/tree/master/ChainOfResponsibilityPattern)
 ```
 // Giao diện trình xử lý khai báo một phương pháp để xây dựng một chuỗi trình xử lý. Nó cũng khai báo phương thức để thực hiện một yêu cầu.
public interface IHandler {
        void AddChain(IHandler handler);
        double Handle(double[] values, string action);
    }
    
// The base class for simple components.
public abstract class BaseHandler : IHandler {
        public void AddChain(IHandler handler) {
            _nextInLine = handler;    
        }

        public abstract double Handle(double[] values, string action);
    }
    
// Các mối quan hệ dây chuyền được thành lập. Class kế thừa override Handler từ cha nó.
public class AdditionHandler : BaseHandler {
        public override double Handle(double[] values, string action) {}
public class MultiplicationHandler : BaseHandler {
        public override double Handle(double[] values, string action) {}
```
- Không có sự thay đổi so với mẫu chuẩn [Chain of Responsibility](https://refactoring.guru/design-patterns/chain-of-responsibility)

## 2.2 Command
- Command biến một yêu cầu thành một đối tượng độc lập chứa tất cả thông tin về yêu cầu. Sự chuyển đổi này cho phép bạn chuyển các yêu cầu dưới dạng đối số của phương thức, trì hoãn hoặc xếp hàng đợi việc thực hiện một yêu cầu và hỗ trợ các hoạt động hoàn tác.
- Code: 
- The base command class xác định giao diện chung cho các concrete commands.
```
internal interface ICommand
    {
        void Execute();
        void Undo();
    }
```
- The concrete commands:
```
internal class GarageDoorCloseCommand : ICommand
    {
        public GarageDoorCloseCommand(Garage g) {...}
        public void Execute() {}
        public void Undo() {}
    }
internal class GarageDoorOpenCommand : ICommand
    {
        public GarageDoorOpenCommand(Garage g) {...}
        public void Execute() {}
        public void Undo() {}
    }
v.v.....
```
- Tất cả các class GarageDoorCloseCommand, GarageDoorOpenCommand, LightOffCommand, LightOnCommand, MacroCommand, NoCommand, .... đều đưuọc xác định từ ICommand nhưng là những đối tượng độc lập, chứa các yêu cầu Execute(), Undo().
- Không có thay đổi so với mẫu chuẩn [Command](https://refactoring.guru/design-patterns/command)

 # 3. Structural Patterns
 ## 3.1 Adapter
 
Được sử dụng trong [AdaptePattern.](https://github.com/abishekaditya/DesignPatterns/tree/master/AdapterPattern)

Các client interface:
IDuck.cs:
```
	public interface IDuck
    {
        void Quack();
        void Fly();
    }
```

ITurkey.cs:
```
public interface ITurkey
    {
        void Gobble();
        void Fly();
    }
```
Method Tester trong class Program.cs tương ứng là methodService.
```
private static void Tester(IDuck duck)
    {
        duck.Fly();
        duck.Quack();
    }
```

Môt instance của ITukey muốn sử dụng Tester phải chuyển đổi sang IDuck thông qua class TurkeyAdapter:
```
    public class TurkeyAdapter : IDuck
    {
    ...
        public void Quack()
        {
             ...
        }

        public void Fly()
        {
            ...
        }
    }
```
Ví dụ với 2 client WildTurkey và TurkeyAdapter

```
    private static void Main()
    {
        var turkey = new WildTurkey();
        var adapter = new TurkeyAdapter(turkey);

        Tester(adapter);
    }
```

Kết luận: hoàn toàn tương đồng so với mẫu thiết kế Adapte, sử dụng adapter để chuyển đổi một instance để phù hợp với service;

## 3.2 Bridge

Được sử dụng trong [BridgePattern.](https://github.com/abishekaditya/DesignPatterns/tree/master/BridgePattern)

Các implementation gồm IEnchantment và IWeapon:
```
    public interface IEnchantment
    {
        void OnActivate();
        void Apply();
        void OnDeactivate();
    }
  
    public interface IWeapon
    {
        void Wield();
        void Swing();
        void Unwield();
        IEnchantment GetEnchantment();
    }
```
Các instance của IEnchantment: SoulEatingEnchantment FlyingEnchantment.
Các instance của IWeapon: Sword, Hammer.

Author đã sử dụng 2 bridge để quán lý 2 thể loại vũ khí là bùa mê (Enchantment) và vũ khí vật lý (Weapon). Các intance sẽ cho biết cách sử dụng và hiệu ứng của từng loại. Giống với mẫu Brigde

Điểm khác: Author có kết hợp sử dụng thêm mẫu Adapter để chuyển đổi IWeapon sang IEnchantment.
```
    public interface IWeapon
    {
        ...
        IEnchantment GetEnchantment();
    }
```

## 3.3 Composite

Được sử dụng trong [CompositePattern.](https://github.com/abishekaditya/DesignPatterns/tree/master/CompositePattern)

Lớp cha MenuComponent gồm các leaf Menu, MenuIteam và Composite là Client.

Ví dụ trong program.cs, Client sử dụng các instance của MenuComponent để quản lý bữa ăn (sửa dụng Menu) và thực đơn trong bữa ăn (MenuIteam).

```
static class Program
    {
        public static void Main()
        {

            var breakfast = new Menu("Breakfast", "Pancake House");
            var lunch = new Menu("Lunch", "Deli Diner");
            var dinner = new Menu("Dinner", "Dinneroni");

            var dessert = new Menu("Dessert", "Ice Cream");

            var menu = new Menu("All", "McDonalds");

            breakfast.Add(new MenuItem("Waffles", "Butterscotch waffles", 140, false));
            breakfast.Add(new MenuItem("Corn Flakes", "Kellogs", 80, true));

            lunch.Add(new MenuItem("Burger", "Cheese and Onion Burger", 250, true));
            lunch.Add(new MenuItem("Sandwich", "Chicken Sandwich", 280, false));

            dinner.Add(new MenuItem("Pizza", "Cheese and Tomato Pizza", 210, true));
            dinner.Add(new MenuItem("Pasta", "Chicken Pasta", 280, false));

            dessert.Add(new MenuItem("Ice Cream", "Vanilla and Chocolate", 120, true));
            dessert.Add(new MenuItem("Cake", "Choclate Cake Slice", 180, false));

            dinner.Add(dessert);
            menu.Add(breakfast);
            menu.Add(lunch);
            menu.Add(dinner);

            menu.Print();
        }
    }
```

Kết luận: Sử dụng mẫu Composite để quản lý các loại Menu, cây tạo ra đơn giản dễ hiểu và hiệu quả.

## 3.4 Facade

Được dùng tại [FacadePattern.](https://github.com/abishekaditya/DesignPatterns/tree/master/FacadePattern)

**Facade** tương ứng với class *HomeTheatreFacade* được dùng để ... gồm các **Subsystem class** : *Dimmer*, *Dvd* và *DvdPlayer*. Với Dimmer quản lý độ sáng của màn hình, Dvd quản lý các moive, DvdPlayer quản lý các tác vụ điều khiển khi xem phim (ví dụ bật, dừng phim).

Kết luận: Author đã sử dụng mẫu Facade để thiết kế các class quản lý từng tác vụ được quản lý chung bới class *HomeTheatreFacade* khi đó Client chỉ cần thao tác với *HomeTheatreFacade* để sử dụng các chứ năng được cung cấp bởi tất cả các subsystem.
Ví dụ trong program.cs:
```
    internal static class Program
    {
        private static void Main()
        {
            var dimmer = new Dimmer();
            var dvdPlayer = new DvdPlayer();
            var dvd = new Dvd("Gone with the Wind 2 : Electric Bugaloo");
            var homeTheater = new HomeTheatreFacade(dimmer, dvd, dvdPlayer);

            homeTheater.WatchMovie();
            Console.WriteLine();
            homeTheater.Pause();
            Console.WriteLine();
            homeTheater.Resume();
            Console.WriteLine();
            homeTheater.Pause();
        }
    }
```

## 3.5 Decorator
Được sử dụng tại [DecoratorPattern](https://github.com/abishekaditya/DesignPatterns/tree/master/DecoratorPattern)

**Component** tương ứng là abstract class *Beverage* khai báo các method chung cho quá trình bao bọc (Mix đồ uống - Description và giá thành - Cost) và đối tượng là đồ uống:

```
    abstract class Beverage
    {
        protected string _description = "No Description";
        public abstract string Description { get; }
        public abstract double Cost();
    }
```
Các **Concrete Component** là các class Espresso, DrakRoast, HouseBlend. Là các đối tượng đồ uống xác định.
ví dụ Espresso.cs
```
class Espresso : Beverage
    {
        public Espresso()
        {
            _description = "Espresso";
        }

        public override string Description => _description;

        public override double Cost()
        {
            return 1.99;
        }
    }
```

**Base Decorator** tương ứng là *Condiment Decorator* có các **Concrete Decorator** tương ứng là  *MochaCondiment*  *WhipCondiment* quản lý việc bổ sung các loại condiment cho đồ uống. 

Điểm khác: Component được sử dụng là abstract class thay vì interface như trong mẫu.

## 3.6 Flyweight
Được sử dụng tại [FlyweightPattern](https://github.com/abishekaditya/DesignPatterns/tree/master/FlyweightPattern)

IBeverage  OolingMilkTea FoamMilkTea CoconutMilkTea BubbleMilkTea 

**Flyweight Factory** tương ứng là class *BubbleTeaShop* đại diện cho một cửa hàng đồ uống quản lý các loại đồ uống - Enumerate(), các hóa đơn - TakeOrders():
```
    private void TakeOrders()
        {
            var factory = new BeverageFlyweightFactory();

            takeAwayOrders.Add(factory.MakeBeverage(BeverageType.BubbleMilk));
            takeAwayOrders.Add(factory.MakeBeverage(BeverageType.BubbleMilk));
            takeAwayOrders.Add(factory.MakeBeverage(BeverageType.CoconutMilk));
            takeAwayOrders.Add(factory.MakeBeverage(BeverageType.FoamMilk));
            takeAwayOrders.Add(factory.MakeBeverage(BeverageType.OolongMilk));
            takeAwayOrders.Add(factory.MakeBeverage(BeverageType.OolongMilk));
        }

        public void Enumerate()
        {
            Console.WriteLine("Enumerating take away orders\n");
            foreach (var beverage in takeAwayOrders)
            {
                beverage.Drink();
            }
        }
```
Có 4 loại đồ uống có khác nhau tương ứng với 4 **Context** :  *BubbleMilk, FoamMilk, OolongMilk, CoconutMilk* có **Flyweight** là *IBeverage*.

Kết luận: Tương đồng với mẫu thiết ké nhưng chưa thể hiện rõ các repeatingState và uniquaState.

## 3.7 Proxy
Được sử dụng tại [ProxyPattern](https://github.com/abishekaditya/DesignPatterns/tree/master/ProxyPattern)

**Service** là RealImg
```
    public class RealImage : Image
    {

        private string _fileName;

        public RealImage(string fileName)
        {
            _fileName = fileName;
            loadFromDisk(_fileName);
        }

        public void display()
        {
            Console.WriteLine("Displaying " + _fileName);
        }

        private void loadFromDisk(string fileName)
        {
            Console.WriteLine("Loading " + fileName);
        }
    }
```
**Service Interface** tương ứng là class Image cung cấp service display() của class RealImg. Và **Proxy** tương ứng là ProxyImg tham chiếu đến display().
```
    public class ProxyImage : Image
    {
    ...
        public void display()
        {
            if (_realImage == null)
            {
                _realImage = new RealImage(_fileName);
            }
            _realImage.display();
        }
    }
```
Kết luận: hoàn toàn tương đồng với mẫu thiết kế, không có sự khác biệt.
