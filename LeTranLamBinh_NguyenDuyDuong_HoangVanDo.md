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
- Link [Abstract Factory](https://github.com/abishekaditya/DesignPatterns/tree/master/FactoryPattern/Abstract%20Factory)
- Ở đây, cung cấp một interface cho việc tạo lập các đối tượng (có liên hệ với nhau) mà không cần qui định lớp khi hay xác định lớp cụ thể (concrete) tạo mỗi đối tượng, 2 class được khai báo theo mẫu chuẩn.
```
internal class ChicagoIngredientsFactory : IIngredientsFactory
internal class NyIngredientsFactory : IIngredientsFactory
```

## 2. Factory Method
- Là một mẫu thiết kế sáng tạo cung cấp một giao diện để tạo các đối tượng trong lớp cha, nhưng cho phép các lớp con thay đổi loại đối tượng sẽ được tạo.
- Link [Factory Method](https://github.com/abishekaditya/DesignPatterns/tree/master/FactoryPattern/Factory%20Method)
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
