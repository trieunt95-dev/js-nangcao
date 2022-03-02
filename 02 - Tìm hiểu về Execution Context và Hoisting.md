# Tìm hiểu về Execution Context và Hoisting

Ở bài viết trước, chúng ta đã tìm hiểu về JS Engine và JS Runtime. Trong bài viết này, chúng ta sẽ cùng nhau tìm hiểu thêm một thuật ngữ mới cũng liên quan đến JS Engine có tên Execution Context, tìm hiểu xem cách nó khởi tạo và xóa bỏ Execution Context như thế nào? Đồng thời, bạn cũng sẽ hiểu về hoisting trong Javascript.

## Execution Context là gì?

Execution Context (Ngữ cảnh thực thi). Context nghĩa là ngữ cảnh, Execution nghĩa là thực thi. Vậy thì khi nói đến thực thi tức là đang nói đến một đoạn chương trình Javascript được chạy thì JS Engine sẽ luôn luôn khởi tạo mới một ngữ cảnh thực thi để theo dõi, giám sát và quản lí trình tự thực thi.

Đoạn chương trình có thể là chương trình chính (Hay nói cách khác là toàn bộ ứng dụng) khi khởi chạy lần đầu tiên hoặc có thể là chương trình con (Trong thuật ngữ của lập trình còn được gọi là Function, Methods của Object nào đó).

-   Chương trình chính: Ngữ cảnh thực thì toàn cục (Global Execution Context)
-   Chương trình con: Ngữ cảnh thực thi cục bộ (Local Execution Context). Bạn có thể ngầm hiểu Execution Context là local nhé.

Trong một ứng dụng thì chỉ có 1 ngữ cảnh thực thi toàn cục (Global) nhưng có thể có nhiều function vì vậy sẽ có nhiều ngữ cảnh thực thi cục bộ (Local). Tuy nhiên, trước khi khởi tạo ngữ cảnh thực thi thì JS Engine sẽ luôn thực hiện 2 giai đoạn:

1. Creation Phase (Giai đoạn khởi tạo)
2. Execution Phase (Giai đoạn thực thi)

Ở giai đoạn Creation Phase này nó sẽ làm rất nhiều việc, một trong số đó là setup memory (Khởi tạo ra biến toàn cục, cục bộ,... để lưu trữ biến, hàm,...) Sau khi khởi tạo xong thì nó mới qua giai đoạn thực thi (Exection Phase). Khi mà chương trình con thực thi xong thì Execution Context sẽ bị xóa bỏ. Đồng thời JS Engine sẽ thu dọn memory mà ở giai đoạn Create Phase đã khởi tạo ra.

Có thể đọc đến đây, sẽ có nhiều bạn chưa hình dung được. Yên tâm, ở phần dưới đây mình sẽ mô phỏng từng bước trong giai đoạn từ lúc nó khởi tạo cho đến khi nó xóa bỏ nên đừng quá lo. Bạn chỉ cần hiểu ý nghĩa của thuật ngữ này là đủ rồi.

## Giai đoạn khởi tạo (Creation Phase)

Ở phần trên, mình đã nói đến khái niệm mới mà trước khi Execution Context được khởi tạo thì nó luôn luôn thực hiện 2 giai đoạn đó chính là Creation Phase và Execution Phase. Tuy nhiên, Execution Phase là giai đoạn nó thực thi nên không có vấn đề gì để nói. Vì vậy nên chúng ta sẽ chỉ tìm hiểu giai đoạn nó khởi tạo hay còn gọi là Creation Phase thôi nhé.

Nếu bạn tìm hiểu sâu về giai đoạn Creation Phase này, bạn sẽ hiểu được những vấn đề như Scope Chain, từ khóa this cũng như là khái niệm về hoisting và cách hoisting hoạt động trong JS.

Trong giai đoạn Creation Phase này, nó sẽ thực hiện 3 việc chính đó là:

1. **Setup Memory (Variables Enviroment):** Ở bước này, nó sẽ setup các biến, hàm, lưu trữ giá trị mà có sử dụng trong chương trình. Phải có bước này thì chương trình mới có thể hoạt động được.
2. **Định nghĩa Scope Chain:** trong JS, có rất nhiều dạng scope (Tầm vực) như: Global Scope, Script Scope, Block Scope và Function Scope
3. **Ràng buộc từ khóa this:** ngoại trừ Arrow Function thì nó cũng sẽ có 3 kiểu ràng buộc:
    - Default Binding (Ràng buộc mặc định)
    - Implicit Binding (Ràng buộc ngầm)
    - Explicit Binding (Ràng buộc tường minh)
