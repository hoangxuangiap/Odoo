***Ngày 1:***

Quy tắc viết mã trong Odoo

1\. Cấu trúc Module



Chứa các thứ mục:

models (chứa logic dữ liệu)

views (chứa giao diện XML)

controllers (chứa mã nguồn web/route)

security (chưa quyền truy cập)

static (chứa CSS, JS, hình ảnh)



File naming:

Chữ thường

Phân cách chữ bằng dấu \_

Không chưa khoảng trắng



**Ngày 2:**

Quy tắc lập trình cốt lõi trong Odoo

1. Quy tắc đặt tên
* Tên Mode: Sử dụng danh từ số ít, phân tách bằng dấu chấm theo cấu xúc không gian của module
* Method Name:Phản ánh chức năng thực hiện của hàm.

2\. Quy tắc thiết kế giao diện XML

Cấu trúc rõ ràng nhất quán: Sắp xếp các thành phần form, tree,kanban theo cấu trúc chuẩn Odoo



**Ngày 3:**



**ORM API:**

Là lớp trung gian chuyển đổi giữa các Python và các bang trong cơ sở dữ liệu PostgreSQL.

Giúp thao tác với dữ liệu thông qua các phương thức Python thay vì viết câu lệnh SQL, đồng thời đảm bảo tính bảo mật và toàn vẹn dữ liệu



**Models:**

* models.Model: Model thông thường, dữ liệu được lưu trữ vĩnh viễn trong cơ sở dữ liệu.
* models.TransientModel: Model tạm thời, dữ liệu tự động bị xóa sau một thời gian
* models.AbstractModel: Model trừu tượng, không tạo bảng trong database, dùng làm lớp cơ sở để chia sẻ mã nguồn và tính năng cho các model khác.



**Fields:**

* Trường cơ bản: Char, Text, Integer, Float, Boolean, Date, Datetime, Binary, Html.



**Trường quan hệ:**

* Many2one: Liên kết nhiều bản ghi về một bản ghi đích.
* One2many: Quan hệ ngược lại của Many2one.
* Many2many: Quan hệ nhiều-nhiều thông qua bảng trung gian.



**Trường đặc biệt:**

Computed Fields: Trường tính toán giá trị bằng hàm Python, có thể lưu trữ hoặc tính động.



Related Fields: Lấy trực tiếp giá trị từ một trường thông qua đường dẫn quan hệ có sẵn.



**Recordsets:**

Là đơn vị cơ bản để xử lý dữ lieu trong Odoo ORM. Một biến recordset có thể đại diện cho 0,1 hoặc nhiều bản ghi.

ORM methods

Các phương thức tiếu chuẩn để thao tác dữ lieu:

&#x20;

* create(vals\_list): Tạo mới bản ghi.
* search(domain): Tìm kiếm bản ghi dựa trên điều kiện lọc và trả về một recordset.
* read(fields): Đọc giá trị các trường được chỉ định.
* write(vals): Cập nhật giá trị cho tập bản ghi.
* unlink(): Xóa bản ghi khỏi cơ sở dữ liệu.
* search\_read(...): Kết hợp tìm kiếm và đọc dữ liệu tối ưu trong một lần gọi.



**Method decoractors**



* @api.depends: Khai báo các trường phụ thuộc để kích hoạt hàm tính toán cho Computed Field.
* @api.onchange: Tự động thay đổi giá trị trên giao diện form ngay khi người dùng thay đổi dữ liệu trường chỉ định (chưa cần lưu database).
* @api.constrains: Kiểm tra tính hợp lệ (validation) của dữ liệu trước khi ghi vào database, nếu sai sẽ báo lỗi UserError.
* @api.model: Đánh dấu phương thức không phụ thuộc vào recordset cụ thể nào (thường dùng cho các hàm khởi tạo hoặc xử lý chung).



**Environment**

Chứa toàn bộ ngữ cảnh hoạt động của hệ thống bao gồm:

* self.env.cr: Con trỏ cơ sở dữ liệu (Cursor) để thực thi câu lệnh SQL trực tiếp khi cần.
* self.env.uid: ID của người dùng hiện tại đang thao tác.
* self.env.user: Đối tượng record của người dùng hiện tại (res.users).
* self.env.context: Từ điển chứa thông tin ngữ cảnh truyền qua lại (ngôn ngữ, múi giờ, trạng thái giao diện).
* self.env\['model.name']: Dùng để gọi và truy cập vào các model khác trong hệ thống.



**Inheritance**

Odoo hỗ trợ các hình thức kế thừa linh hoạt để mở rộng ứng dụng sẵn có:

* Class Inheritanxe: kế thừa và mở rộng trực tiếp ứng dụng sẵn có.
* Prototype Inheritance: Kế thừa toàn bộ trường và phương thức từ một model khác nhưng tạo ra bảng dữ liệu riêng biệt.
* Delegation (\_inherits): Ủy quyền dữ liệu sang một model khác thông qua mối quan hệ Many2one, giúp tái sử dụng thông tin của bảng cha.



**View:**

View trong Odoo là một cấu trúc XML mổ tả giao diện hiểm của car đổi tượng dữ Liệu

Tính kế thừa: Các view có thể kế thừa lẫn nhau, để them bớt, chỉnh sửa thành phần giao diện của 1 view sẳn có mà không câng biết lại từ dâu

Kiểu dữ liệu: mỗi view nhắm tối mô hình vụ thể.



**Các loại View chính trong Bachend:**



* List View:

Hiển thị danh sách các bang ghi dưới dạng (hang và cột.



* Form View:

Hiển thị chi tiết một bản ghi đơn lẻ.



* Kanban View:

Hiển thị dữ liệu trực quan thoe các thẻ, thường dung để quản trị quy trình, trạng thái công việc.



* Search View:

Thanh tìm kiếm và bộ lọc dữ liệu nằm phía trên cùng của Lisf/Kanban.



**Các thuộc tính và Thẻ XML quan trọng trên Form/List View.**



Thuộc tính điều khiển giao diện:



invisible="1": Ẩn trường hoặc thành phần trên giao diện.



readonly="1": Khóa không cho chỉnh sửa trường dữ liệu.



required="1": Bắt buộc phải nhập dữ liệu trước khi lưu.



**Ngày 4:**



**Actions trong Odoo**

Actions xác định hệ thống phản hồi lại các tương tác của người dung

1. **Các thuộc tính bắt buộc của một Action**

type: Phân loại action, quyết định cách hệ thống phân tích và xử lý đối tượng.

name: Tên hiển thị ngắn gọn của action mục địch quản lý và đọc hiểu.



**2 Các loại Action phổ biến**

* Window Actions

là loại phổ biến nhất dùng để hiển thị dữ lieu của Model lên giao diện người dùng dạng View (List,Form,Kanban...).

* Url Action

Điều hướng trình duyệt của người dùng đến một địa chỉ web(Url) bên ngoài 1 trang web tích hợp.

Có thể tích hợp mở liên kết trên 1 tab trình duyệt mới hoặc chuyển hướng trực tiếp trang hiện tại.

* Server Actions

Cho phép hệ thống tự động các đoạn mã Python, tự động tạo mới/cập nhật bản ghi, hoặc chuỗi hành động hết hợp ở phía server mà không cần qua giao diện thủ công.

* Report Actions:

Dùng để gọi tiến trình in ấn hoặc xuất dữ lieu báo cáo.

* Client Actions:

Gọi trực tiếp mọt hành động hoặc một ứng dụng chạy hoàn toàn ở phía trình duyệt.

Được sử dụng để tích hợp các thành phần giao diện nâng cao được viết bang JS.

* Automated Actions

Tự động kích hoạt các Server Actions dựa trên các sự kiện hoặc mốc thời gian diễn ra trong cơ sở dữ lieu.



**Security**

Security của Odoo được thiết kế đa tang nhắm kiểm soát chat chẽ quyền truy cập vào dữ lieu và tính năng của hệ thống.



**Nhóm quyền.**

Mục đích: Phân chia người dùng vào các nhóm chức năng khác nhau

Các nhóm có thể kế thừa lẫn nhau để tạo ra phân cấp quyền từ thấp đến cao.



1. Access Right

Xác định quyền thao tác cơ bản của 1 nhóm người dùng đối với toàn bộ một Model cụ thể.

Được khai báo thông qua tệp cấu hình

4 quyền được thao tác chính:

perm\_read: Quyền đọc, xem dữ lieu của bản ghi.

perm\_write: Quyền chỉnh sửa, cập nhật thông tin bản ghi.

perm\_create: Quyền tạo mới bản ghi.

perm\_unlink: Quyền xóa bản ghi khỏi hệ thống.



2\. Quy tắc bản ghi (Access rules)

Dùng để lọc giới hạn quyền truy cập ở cấp độ từng bản ghi riêng lẻ thay vì kiểm soát mọi thứ trong model.

Sử dụng biểu thức mien dữ lieu để quyết định bản ghi nào người dùng thuộc nhóm đó được phép xem, sửa, xóa.



3\. Group (Nhóm quyền)

Đối tượng đại diện cho 1 tập hợp người dùng có chung chức năng và vai trò trong hệ thống.

Cơ chế phân cập: Các nhóm quyền có thể kế thừa lẫn nhua thông qua thuộc tính implied\_ids ,giúp thiết lập cấu trúc phân quyền từ cấp độ thâp lên cấp độ cao

Ứng dụng: Làm căn cứ để gắn kết với Access Right, Record Rules hoặc dùng để ẩn/hiện các nút bấm, trường dữ liệu trên giao diện XML.



**Ngày 5**



1. Controllers

Các yêu cầu HTTP gửi đến Odoo được xử lý bởi các Controllers. Để trọa một controllers, bạn cần định nghĩa một lớp Python kể thừ từ http.Controller.

Đăng ký URL: Sử dụng decorator để liên kết 1 phương thức Python với 1 đường dẫn URL cụ thể trên hệ thống.



2\. Cấu trúc dectorator

Decorator hỗ trợ nhiều tham số quan trọng để cầu hình hành vi của route:

* route: ĐƯờng dẫn URL
* type: Loại giao thức xử lý yêu cầu

  * 'http': Xử lý các yêu cầu gọi hàm từ xa thông qua JSON-RPC.
* auth: Mức độ xác thực người dùng khi truy cập

  * 'user': Người dùng bắt buộc phải đăng nhập vào hệ thống.
  * 'public': Cho phép cả khách vãng lai hoặc người dùng đã đăng nhập truy cập.
  * 'none': Không yêu cầu xác thục phên làm việc hoặc cơ sở dữ liệu
* methods: Giới hạn phương thức HTTP được phép.
* csrf: Cho phép bật hoặc tắt kiểm tra mã bảo mật CSRF.



QWeb

Là hệ thống template chính được Odoo sử dụng.Qweb là các tệp XML được biệc dịch thành hàm JavaScrip hoặc mã Python để render dữ liệu thành HTML.



1. Điều khiển chính trong QWeb
* Hiển thị dữ liệu: Dùng để in giá trị cảu một biến ra HTML
* Hiển thị HTML thô (t-raw): In chuổi dữ liệu dưới dạng mã HTML nguyên bản.
* Điều kiện rẽ nhánh: Xây dựng logic điều kiện tương tự cấu lệnh if-else trong lập trình.
* Vòng lặp: Duyệt qua danh sách các bản ghi hoặc từ điển dữ liệu. Trong vòng lặp, Odoo tự động cung cấp các biến phụ trợ như \_all, \_even, \_odd, firsr, last.
* Gán biến: Định nghĩa hoặc thay đổi giá trị của 1 biến trong phạm vi template.

2\. Thao tác thuộc tính và nội dung linh hoạt

* Gắn thuộc tính động (t-att... hoặc t-attf-...):

t-att-class="variable": Gắn giá trị thuộc tính động hoàn toàn từ biến.

t-attf-class="my-class" {{ variable}} ">: Gắn thuộc tính kết hợp giữa chuỗi tĩnh và biểu thức động.

* Kết hợp phần tử HTML(t-field): Dùng cho các trường dữ liệu của Model Odoo để tự động định dạng hiển thị và hỗ trợ chỉnh sửa trực tiếp.



**Ngày 6:**

JavaScript In Odoo

1. Owl Framework Components

Toàn bộ giao diện người dùng phía client đều được xây dựng dựa trên các component của Owl.

Cấu trúc Component: Mỗi component thường gồm 1 lớp JavaScrip kết hợp với 1 template Qweb được viết bằng cú pháp XML tương tự như JSX để render giao diện trực quan.



2\. Khái niệm cốt lõi

* Assets Management

Cơ chế khai báo, gom nhóm và các tệp như JS, CSS/SCSS và các tệp template XML lên trình duyệt. 

* Module System

Cơ chế quản lý phạm vi và phụ thuộc giữa các tệp JS trong Odoo.

Odoo sử dụng hệ thống danh mục Module giữa các tệp JS có thể gọi, Kế thừa và tái sử dụng lẫn nhau mà không làm ô nhiễm biến toàn cục.

* Inheritance, Mixins, Patching( Kế thừa và vá lỗi)

Inheritanca, Patching: Thay vì kế thừa lớp phức tạp như backend Python, ở frontend, Odoo cung cấp hàm patch cho phép lập trình viên ghi đè, mở rộng hoặc bổ sung phương thức cho các component hoặc đối tượng sẵn có của Odoo mà không cần viết lại toàn bộ.

Mixins: Các đoạn mã logic độc lập có thể được trộn vào nhiều component khác nhau để tái sử dụng các tính năng chung.

* Widget

Mỗi component là một khối giao diện độc lập gồm mội lớp JS kết hợp với một template XML. Component có vòng đời rõ ràng với các loại hook chuẩn như setup(), onWillStart(), onMounted().

* Even

DOM Events: lắng nghe và xử lý các thao tác tương tác của người dùng trực tiếp trên giao diện thông qua cú pháp khai báo trong template XML.

Component Events: Cơ chế truyền tín hiệu giữa các component

* Fields Widget

Các component chuyên biệt dùng để hiển thị và tương tác với các kiểu dữ liệu cụ thể (như Char, Integer,Many2one,Binary) trên các dạng giao diện Form hoặc List.









