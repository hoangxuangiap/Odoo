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



Ngày 3:



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

