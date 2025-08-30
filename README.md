# 🧹 Clean code in Unity
## ❓ Clean code là gì? Tại sao cần clean code?

- Clean code (mã sạch) là một khái niệm trong lập trình phần mềm, đề cập đến việc viết mã nguồn sao cho dễ đọc, dễ hiểu và
  dễ bảo trì.
- Mục tiêu của clean code là giúp các lập trình viên khác (hoặc chính bạn trong tương lai) có thể nhanh chóng
  hiểu được ý định của mã nguồn, giảm thiểu lỗi và tăng hiệu suất làm việc.

## 🚀 Clean code nên bắt đầu từ đâu?

1. 🏷️ **Đặt tên biến và hàm rõ ràng**:
    - Một tên biến/hàm được xem là tốt khi các lập trình viên khác nhau đọc đều có thể hiểu được biến/hàm đó
      dùng để làm gì.
    - Tên biến và tên hàm phải là tên có nghĩa
    - Chữ cái đầu tiên của biến sẽ là chữ thường, các chữ cái đầu tiên của các từ tiếp theo sẽ viết hoa (ví dụ:
      `string studentName = "VirtueSky";`, `int calculateTotal = 0`).
    - Không sử dụng tên có ký tự đầu tiên là số (ví dụ: `int d = 365;`)
    - Đối với tên hàm cũng tương tự tuy nhiên chữ cái bắt đầu của tên hàm sẽ là chữ in hoa, (ví dụ: `GetDayInYear(){}`)
    - Không viết tắt trong tên biến hoặc tên hàm.
    - Sử dụng tên biến nhất quán trong suốt project
      (ví dụ: `const int DAYS_IN_WEEK = 7;` or `const int daysInWeek = 7;`) trong 2 kiểu tên biến const ở ví dụ, nếu đã
      follow theo kiểu nào sẽ làm tương tự xuyên suốt project.
2. 🔀 **If-Else và Switch-case**
   - Cân nhắc trong các trường hợp có nhiều nhánh (10-20 case) và điều kiện kiểm tra là các giá trị rời rạc của cùng một biến (enum, int, string, v.v...) thì nên sử dụng switch-case thay vì if-else.
   - Việc sử dụng switch-case sẽ giúp code dễ đọc hơn, dễ bảo trì và mở rộng hơn trong tương lai.
   - Switch-case sẽ nhảy thẳng vào điều kiện đúng mà không cần phải kiểm tra lần lượt từng điều kiện như if-else => hiệu năng cũng tốt hơn.
3. 🚫 **Nói không với hard code**
    - Hard code là việc bạn gán trực tiếp một giá trị cụ thể vào trong mã nguồn thay vì sử dụng biến hoặc hằng số.
    - Việc sử dụng hard code sẽ làm cho mã nguồn trở nên đọc khó hiểu và khó bảo trì.
    - Đối với Unity, đôi khi bạn nên tạo các tuỳ chỉnh để có thể thay đổi dễ dàng ngoài editor thay vì phụ thuộc vào script.
    - 👉Ví dụ: 
        ```csharp
        // Hard code
        void Start() {
            transform.position = new Vector3(0, 10, 0);
        }
    
        // Clean code
        public Vector3 startPosition = new Vector3(0, 10, 0);
        void Start() {
            transform.position = startPosition;
        }
        ```
4. 🔧 **Mỗi hàm nên thực hiện một tính năng duy nhất**
    - Một hàm nên được thiết kế để thực hiện một nhiệm vụ cụ thể và rõ ràng.
    - Nếu một hàm thực hiện quá nhiều nhiệm vụ, nó sẽ trở nên khó đọc và khó bảo trì (ví dụ một hàm thực hiện xử lý đồng thời input, update animation, tính toán vật lý).
    - Nên chia nhỏ hàm lớn thành các hàm nhỏ hơn, mỗi hàm đảm nhận một nhiệm vụ cụ thể.
    - 👉Ví dụ:
        ```csharp
        // Bad example
        void Update() {
            // Xử lý input
            // Cập nhật animation
            // Tính toán vật lý
        }
    
        // Good example
        void Update() {
            HandleInput();
            UpdateAnimation();
            CalculatePhysics();
        }
    
        void HandleInput() {
            // Xử lý input
        }
    
        void UpdateAnimation() {
            // Cập nhật animation
        }
    
        void CalculatePhysics() {
            // Tính toán vật lý
        }
        ```
      
5. 📝 **Sử dụng comment một cách hợp lý**
    - Comment nên được sử dụng để giải thích "tại sao" một đoạn mã được viết như vậy.
    - Tránh việc comment quá nhiều hoặc comment những điều hiển nhiên trong mã nguồn.
    - Nếu bạn thấy mình cần phải comment quá nhiều để giải thích mã nguồn, có thể mã nguồn đó cần được viết lại cho rõ ràng hơn.
    - 👉Ví dụ:
      ```csharp
         /// <summary>
         /// This function calculates the sum of two integers.
         /// </summary>
         /// <param name="a">First integer</param>
         /// <param name="b">Second integer</param>
         /// <returns></returns>
         int CalculateTotal(int a, int b) 
         {
            return a + b;
         }
      ```
6. 🎭 **Sử dụng enum để dễ dàng phân loại**
    - Enum là một kiểu dữ liệu đặc biệt trong C# cho phép bạn định nghĩa một tập hợp các hằng số có tên.
    - Sử dụng enum giúp mã nguồn trở nên rõ ràng hơn và dễ bảo trì hơn so với việc sử dụng các giá trị số nguyên hoặc chuỗi để đại diện cho các trạng thái hoặc loại khác nhau.
    - 👉Ví dụ:
      ```csharp
         // Bad example
         int playerState = 1; // 1: Idle, 2: Running, 3: Jumping
    
         // Good example
         enum PlayerState 
         {
            Idle,
            Running,
            Jumping
         }
    
         PlayerState playerState = PlayerState.Idle;
      ```
7. 🗂️ **Không bỏ ngoặc trong if-else, for**
    - Dù chỉ có một dòng lệnh trong khối if-else, for thì vẫn nên sử dụng ngoặc nhọn `{}` để bao quanh khối lệnh đó.
    - Việc này giúp tránh các lỗi không mong muốn khi bạn hoặc người khác thêm dòng lệnh mới vào khối lệnh sau này.
    - 👉Ví dụ:
      ```csharp
         // Bad example
         if (isGameOver)
            Debug.Log("Game Over");
    
         // Good example
         if (isGameOver) 
         {
            Debug.Log("Game Over");
         }
      ```
8. ⚠️ **Không lạm dụng Singleton**
    - Singleton là một mẫu thiết kế (design pattern) dễ tiếp cận và dễ dùng, nó cho phép bạn đảm bảo rằng một lớp chỉ có một thể hiện duy nhất và cung cấp một điểm truy cập toàn cục đến thể hiện đó.
    - Mặc dù singleton có thể hữu ích trong một số trường hợp, nhưng việc lạm dụng nó có thể dẫn đến mã nguồn khó đọc, khó bảo trì và khó kiểm thử do có reference chồng chéo khắp nơi trong project.
    - Nên sử dụng singleton một cách cẩn thận và chỉ khi thực sự cần thiết. Trong một số trường hợp, bạn có thể cân nhắc để kết hợp với một số pattern khác như Observer hoặc Dependency Injection để giảm sự phụ thuộc vào singleton.
9. 🏗️ **Vận dụng tốt lập trình hướng đối tượng**
    - Lập trình hướng đối tượng (OOP) là một phương pháp lập trình dựa trên việc tổ chức mã nguồn thành các đối tượng có trạng thái và hành vi riêng.
    - Sử dụng OOP giúp mã nguồn trở nên dễ đọc, dễ bảo trì và dễ mở rộng hơn.
    - Một số nguyên tắc cơ bản của OOP bao gồm:
        - **Encapsulation (Đóng gói)**: Giữ trạng thái và hành vi của đối tượng bên trong lớp và chỉ cho phép truy cập thông qua các phương thức công khai.
        - **Inheritance (Kế thừa)**: Tạo các lớp con từ lớp cha để tái sử dụng mã nguồn và mở rộng chức năng.
        - **Abstraction (Trừu tượng)**: Tạo các lớp trừu tượng để định nghĩa giao diện chung cho các lớp con.
        - **Polymorphism (Đa hình)**: Cho phép cùng một hành động (phương thức) nhưng có thể thực hiện theo nhiều cách khác nhau, tùy thuộc vào đối tượng cụ thể đang sử dụng...
    - 👉Ví dụ 1: Sử dụng kế thừa để tái sử dụng mã nguồn và giảm sự lặp lại
      ```csharp
         // Bad example
         class Player 
         {
            public string name;
            public int health;
            public void Move() { /* ... */ }
            public void Attack() { /* ... */ }
            public void Defend() { /* ... */ }
         }
    
         // Good example
         class Character 
         {
            public string name;
            public int health;
            public void Move() { /* ... */ }
         }
    
         class Player : Character 
         {
            public void Attack() { /* ... */ }
            public void Defend() { /* ... */ }
         }
      ```
    - 👉Ví dụ 2: Lợi ích của việc sử dụng (trừu tượng) interface để giảm sự phụ thuộc vào các lớp cụ thể
      - Bad example
      ```csharp
        public class BlueMonster : MonoBehaviour
        {
            public void TakeDamage(int amount)
            {
                Debug.Log("Blue Monster took " + amount + " damage!");
            }
        }
        public class RedMonster : MonoBehaviour
        {
            public void TakeDamage(int amount)
            {
                Debug.Log("Red Monster took " + amount + " damage!");
            }
        }
        public class GreenMonster : MonoBehaviour
        {
            public void TakeDamage(int amount)
            {
                Debug.Log("Green Monster took " + amount + " damage!");
            }
        }

        public class Player : MonoBehaviour
        {
            public int damage;
            private void OnTriggerEnter(Collider other)
            {
                if (other.GetComponent<BlueMonster>() != null)
                {
                    // Handle BlueMonster collision
                    other.GetComponent<BlueMonster>().TakeDamage(damage);
                }
                else if(other.GetComponent<RedMonster>() != null)
                {
                    // Handle RedMonster collision
                    other.GetComponent<RedMonster>().TakeDamage(damage);
                }
                else if(other.GetComponent<GreenMonster>() != null)
                {
                    // Handle GreenMonster collision
                    other.GetComponent<GreenMonster>().TakeDamage(damage);
                }
            }
        }

      ```
      - Good example
      ```csharp
        public interface IMonster
        {
            void TakeDamage(int amount);
        }

        public class BlueMonster : MonoBehaviour, IMonster
        {
            public void TakeDamage(int amount)
            {
                Debug.Log("Blue Monster took " + amount + " damage!");
            }
        }
        public class RedMonster : MonoBehaviour, IMonster
        {
            public void TakeDamage(int amount)
            {
                Debug.Log("Red Monster took " + amount + " damage!");
            }
        }
        public class GreenMonster : MonoBehaviour, IMonster
        {
            public void TakeDamage(int amount)
            {
                Debug.Log("Green Monster took " + amount + " damage!");
            }
        }

        public class Player : MonoBehaviour
        {
            public int damage;
            private void OnTriggerEnter(Collider other)
            {
                if (other.GetComponent<IMonster>() != null)
                {
                    // Handle BlueMonster collision
                    other.GetComponent<IMonster>().TakeDamage(damage);
                }
            }
        }
      ```
      - Trong ví dụ trên, việc sử dụng interface `IMonster` giúp giảm sự phụ thuộc của lớp `Player` vào các lớp cụ thể như `BlueMonster`, `RedMonster`, và `GreenMonster`. 
        Điều này làm cho mã nguồn trở nên linh hoạt hơn và dễ bảo trì hơn trong tương lai.
        Hoặc nói dễ hiểu hơn là giúp bạn không phải if-else gãy tay đến ch*t trong `OnTriggerEnter` khi bạn có thêm 20 loại monster mới...
      - Các ví dụ trên chỉ là một số ứng dụng cơ bản của OOP trong việc clean code, bạn hãy hiểu kỹ và vận dụng thật linh động cho nhiều trường hợp khác.

10. 📐 **Tuân thủ quy tắc SOLID**
    - `SOLID` là một tập hợp các nguyên tắc thiết kế phần mềm giúp tạo ra mã nguồn dễ bảo trì, mở rộng và tái sử dụng.
    - Các nguyên tắc SOLID bao gồm:
      - **Single Responsibility Principle (SRP)**: Mỗi lớp nên chỉ có một lý do để thay đổi, tức là mỗi lớp nên chỉ đảm nhận một nhiệm vụ duy nhất.
      - **Open/Closed Principle (OCP)**: Các lớp nên được mở để mở rộng nhưng đóng để sửa đổi, tức là bạn nên có thể thêm chức năng mới mà không cần thay đổi mã nguồn hiện có.
      - **Liskov Substitution Principle (LSP)**: Các đối tượng của lớp con nên có thể thay thế cho các đối tượng của lớp cha mà không làm thay đổi tính đúng đắn của chương trình.
      - **Interface Segregation Principle (ISP)**: Nên tạo các giao diện nhỏ và cụ thể thay vì các giao diện lớn và chung chung, để các lớp chỉ cần triển khai những phương thức mà chúng thực sự cần.
      - **Dependency Inversion Principle (DIP)**: Các lớp cấp cao không nên phụ thuộc vào các lớp cấp thấp, cả hai nên phụ thuộc vào các trừu tượng. Trừu tượng không nên phụ thuộc vào chi tiết, chi tiết nên phụ thuộc vào trừu tượng.
    
    - 👉Ví dụ 1 (SRP): Một class sẽ mang một nhiệm vụ duy nhất
      - Bad example: Class `InvoiceService` gộp tính toán và lưu file
         ```csharp
            class InvoiceService {
                 public decimal CalculateTotal(IEnumerable<decimal> items) => items.Sum();
                 public void SaveToDisk(string path, string content) => File.WriteAllText(path, content);
             }
         ```
      - Good example: Tách riêng tính toán và lưu file thành hai class khác nhau
        ```csharp
           class InvoiceCalculator {
                public decimal CalculateTotal(IEnumerable<decimal> items) => items.Sum();
           }

           class FileSaver {
                public void SaveToDisk(string path, string content) => File.WriteAllText(path, content);
           }
        ```
    - 👉Ví dụ 2 (OCP): Dễ mở rộng, hạn chế sửa code cũ.
      - Bad example: Mỗi khi thêm một hình thì phải sửa switch để tính diện 
      ```csharp
         double Area(string shape, params double[] p)
         {
            return shape switch
            {
               "circle" => Math.PI * p[0] * p[0],
               "rect"   =>  p[0]*p[1]
            };
         }
      ```
      - Good example: Mỗi khi thêm một hình mới chỉ cần tạo class mới kế thừa từ Shape và tính tổng thông qua trừu tượng interface IShape
      ```csharp
        interface IShape { double Area(); }

        class Circle : IShape
        {
            double r;
            public double Area() => (double)Math.PI * r * r;
        }

        class Rect : IShape
        {
            double w, h;
            public double Area() => w * h;
        }

        // thêm Triangle chỉ cần class mới, không sửa code cũ
        class Triangle : IShape
        {
            double b, h;
            public double Area() => b * h / 2;
        }
        
        // Lúc này để tính tổng diện tích thì cũng chỉ cần duyệt thông qua mảng IShape
        class AreaCalculator
        {
            public double TotalArea(IShape[] shapes)
            {
                double area = 0;
                foreach (var shape in shapes)
                    area += shape.Area();
                return area;
            }
        }
      ```
    - 👉Ví dụ 3 (LSP): Class con thay thế class cha mà không phá logic.
      - Bad example: Chim cánh cụt không biết bay nhưng vẫn bị ép thừa kế `Fly()`
      ```csharp
        abstract class Bird
        {
            public abstract void Fly();
        }

        class Sparrow : Bird
        {
            public override void Fly() {}
        }

        // sai LSP
        class Penguin : Bird
        {
            public override void Fly() { throw new NotSupportedException(); }
        } 
      ```
      - Good example: Tách khả năng bay ra interface 
      ```csharp
        abstract class Bird
        {
            public string Name { get; set; } = "";
        }

        interface IFlyable
        {
            void Fly();
        }

        class Sparrow : Bird, IFlyable
        {
            public void Fly() { /* ... */ }
        }

        class Penguin : Bird
        {
             /* không bay, vẫn ok */
        }         
      ```
    - 👉Ví dụ 4 (ISP): Tách interface lớn thành các interface nhỏ hơn.
        Việc này bản chất cũng giống vị dụ trên để tránh implement những method thừa và không cần thiết.
      - Bad example: Interface “đa năng”, class phải implement hàm không dùng
      ```csharp
        interface IMachine
        {
            void Print(); 
            void Scan(); 
            void Fax();
        }
        class SimplePrinter : IMachine {
            public void Print() {}
            public void Scan() { /* trống */ }
            public void Fax() { /* trống */ }
        }
      ```
      - Good example: Tách nhỏ để có thể tuỳ biến implement theo nhu cầu
      ```csharp
        interface IPrinter
        {
            void Print();
        }

        interface IScanner
        {
            void Scan();
        }

        interface IFax
        {
            void Fax();
        }

        class SimplePrinter : IPrinter
        {
            public void Print() {}
        }

        class MultiFunction : IPrinter, IScanner, IFax
        {
            public void Print() {}
            public void Scan() {}
            public void Fax() {}
        }
      ```
    - 👉Ví dụ 5 (DIP): Phụ thuộc abstraction (interface), không phụ thuộc class cụ thể.
      - Bad example: Set cứng vào EmailNotifier
      ```csharp
        class EmailNotifier
        {
            public void Send(string msg) {}
        }

        class OrderService {
            private readonly EmailNotifier _notifier = new();
            public void PlaceOrder() { /* ... */ _notifier.Send("OK"); }
        }
      ```
      - Good example: Phụ thuộc interface INotifier, dễ dàng thay đổi cách thông báo khác (SMS, Push...). 
          Cách này người ta thường gọi là `Tiêm qua interface`.
      ```csharp
        interface INotifier
        {
            void Send(string msg);
        }

        class EmailNotifier : INotifier
        {
            public void Send(string msg) {}
        }

        class SmsNotifier : INotifier
        {
            public void Send(string msg) {}
        }

        class OrderService 
        {
            private INotifier _notifier;

            public void Initialize(INotifier notifier)
            {
                _notifier = notifier;
            }
            public void PlaceOrder() { /* ... */ _notifier.Send("OK"); }
        }
      ```

11. 🧩 **Sử dụng partial class để mở rộng**
    - Partial class là một tính năng trong C# cho phép bạn chia một lớp thành nhiều phần trong các tệp khác nhau.
    - Sử dụng partial class giúp mã nguồn trở nên sạch hơn và dễ bảo trì hơn, đặc biệt khi một lớp có nhiều chức năng hoặc khi bạn muốn tách riêng các phần của lớp để dễ dàng quản lý.
    - Việc này rất hiệu quả khi có nhiều người cùng làm feature và cần tách riêng code của mình ra để tránh xung đột.
    - 👉Ví dụ:
      ```csharp
         // File Character.Movement.cs
         public partial class Character : MonoBehaviour
         {
             public void Move() { /* ... */ }
         }

         // File Character.Combat.cs
         public partial class Character : MonoBehaviour
         {
             public void Attack() { /* ... */ }
             public void Defend() { /* ... */ }
         }

         // File Character.Inventory.cs
         public partial class Character : MonoBehaviour
         {
             public void AddItem(string item) { /* ... */ }
             public void RemoveItem(string item) { /* ... */ }
         }
      ```

12. 🎯 **Hãy chọn một pattern chính xuyên suốt**
    - Trong lập trình, có rất nhiều design pattern khác nhau như Singleton, Factory, Observer, Strategy, v.v...
    - Mỗi pattern đều có ưu điểm và nhược điểm riêng, và không phải pattern nào cũng phù hợp với mọi tình huống.
    - Việc chọn một pattern chính để áp dụng xuyên suốt trong project sẽ giúp mã nguồn trở nên nhất quán hơn và dễ bảo trì hơn.
    - Ví dụ: Nếu bạn chọn sử dụng pattern Observer để quản lý sự kiện trong game, hãy cố gắng áp dụng nó cho tất cả các hệ thống liên quan đến sự kiện thay vì sử dụng nhiều pattern khác nhau.
13. 🎨 **Sử dụng một kiểu format code cho toàn bộ project**
    - Việc sử dụng một kiểu format code nhất quán trong toàn bộ project sẽ giúp mã nguồn trở nên dễ đọc và dễ bảo trì hơn. Đây là một cách hiệu quả cho những người OCD giảm sự khó chịu =))
    - Các IDE bây giờ đều hỗ trơ rất tốt việc này. Có 2 kiểu format phổ biến trong c# là K&R style và BSD style, hãy chọn cho mình một kiểu phù hợp
    - Điều quan trọng là tất cả các thành viên trong team đều phải tuân thủ quy tắc này để đảm bảo tính nhất quán trong mã nguồn.
14. 📦 **Dùng ScriptableObject thay vì hard code data**
    - ScriptableObject là một loại đối tượng trong Unity cho phép bạn lưu trữ dữ liệu một cách dễ dàng và hiệu quả.
    - Sử dụng ScriptableObject để lưu trữ dữ liệu thay vì hard code trực tiếp trong script sẽ giúp mã nguồn trở nên sạch hơn và dễ bảo trì hơn.
    - Thay vì hard code các thuộc tính của một nhân vật trong script, bạn có thể tạo một ScriptableObject để lưu trữ các thuộc tính này và dễ dàng chỉnh sửa chúng trong editor.
    - 👉Ví dụ:
      ```csharp
         // Tạo ScriptableObject để lưu trữ dữ liệu nhân vật
         [CreateAssetMenu(fileName = "NewCharacterData", menuName = "Character Data", order = 51)]
         public class CharacterData : ScriptableObject
         {
             public string characterName;
             public int health;
             public int attackPower;
         }

         // Sử dụng ScriptableObject trong script
         public class Character : MonoBehaviour
         {
             public CharacterData characterData;

             void Start()
             {
                 Debug.Log("Character Name: " + characterData.characterName);
                 Debug.Log("Health: " + characterData.health);
                 Debug.Log("Attack Power: " + characterData.attackPower);
             }
         }
      ```
