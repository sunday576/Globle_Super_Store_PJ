# Globle_Super_Store_PJ
## Data Preparation
* Thu thập dữ liệu: Bộ dữ liệu Global Super Store Dataset 2016 được thu thập thông qua đường link sau: https://powerbidocs.com/2019/11/28/power-bi-sample-data-set-for-practice/

## Data Understanding
* Mô tả dữ liệu
  - Bảng Order: Gồm 24 trường dữ liệu và 51290 dòng dữ liệu
    + Row_ID: Số thứ tự dòng
    + Order_ID: Mã đơn đặt hàng
    + Order_Date: Ngày đặt hàng
    + Ship_Date: Ngày giao hàng
    + Ship_Mode: Phương thức vận chuyển cho đơn hàng
    + Customer_ID: Mã khách hàng 
    + Customer_Name: Tên khách hàng
    + Segment: Phân khúc khách hàng
    + Postal_Code: Mã bưu chính
    + City: Thành phố
    + State: Tiểu bang
    + Country_Region: Khu vực (vd: miền Bắc, Nam,...)
    + Market: Khu vực thị trường
    + Product_ID: Mã sản phẩm
    + Category: Danh mục sản phẩm
    + Sub-Category: Danh mục phụ của sản phẩm
    + Product_Name: Tên sản phẩm
    + Sales: Doanh thu từ sản phẩm
    + Quantity: Số lượng đã đặt của mỗi sản phẩm
    + Discount: Giảm giá áp dụng cho sản phẩm đã mua
    + Profit: Lợi nhuận thu được từ sản phẩm 
    + Shipping_Cost: Chi phí vận chuyển đơn hàng
    + Order_Priority: Thứ tự ưu tiên của đơn hàng.
## Data Preprocessing
* Dữ liệu được thu thập không bao gồm các dòng giá trị trùng lặp và không có missing value nên không cần xử lý thêm ở bước này.
* Ta sẽ tiến hành bỏ một số cột không cần thiết để thuận tiện cho quá trình phân tích cũng như giảm độ phức tạp của bài toán : Row_ID, Postal_Code, State, Market, Order_Priority --> ta thu được bộ dữ liệu mới gồm 19 cột và số dòng giữ nguyên.

## Data Modeling
Ở bước này ta sẽ tiến hành xây dựng biểu đồ sao (star schema) với bảng Fact là Orders và các bảng Dim được tách ra từ các trường dữ liệu của bảng Orders.

### Xây dựng bảng Dim
* Bảng Sub-Category:
  - Tạo một sheet mới trong Excel tên là Sub-Category
  - Copy cột Sub_Category từ bảng Orders sang sheet mới và tạo thêm một cột SubCate_ID
    
  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/43bcd6dc-af3c-41c8-9cf8-b7de7eddfca8)

  
  - Loại bỏ các giá trị trùng lặp trong cột Sub-Category để lọc ra những danh mục phụ và thu được kết quả như sau

   ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/ad5798a0-96bf-4533-b25c-4f2207895748)


  - Tiến hành tạo SubCate_ID bảng cách lấy 3 ký tự đầu tiên từ trái sang như sau:

  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/ad53dd34-da21-4e59-9979-041f41345630)


  - Copy và Paste chỉ lấy giá trị thu được vào Subcate_ID tương ứng
  - Tiến hành lưu vùng giá trị thu được dùng Define name:

  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/d7a81396-9687-4df4-a614-79915203802a)


* Bảng Category:
  - Tạo một sheet mới trong Excel tên là Category
  - Copy cột Category và Sub-Category từ bảng Oders sang và thêm 2 cột Category_ID và SubCate_ID như sau:
    
  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/30f5f01d-e8b1-4caa-ad3d-8bea2040aac6)

  - Dùng Vlookup để điền Subcate_ID tương ứng và loại bỏ các giá trị trùng lặp tương tự như trên, ta thu được kết quả sau:

  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/e1b49928-02e9-40fd-9800-ab412663b36f)

  - Loại bỏ các giá trị trùng lặp tương tự như trên, ta thu được kết quả sau:

  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/170ab23e-f58e-4c84-b8dc-297ed42d856e)

  - Xóa cột Sub-Category và tiến hành tạo Category_ID bằng cách lấy 3 ký tự đầu tiên từ trái sang, ta thu được kết quả:

   ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/a9c1e8d4-f320-4136-b6d1-f9a87c3b6553)

  - Copy và Paste chỉ lấy giá trị với cột Category_ID và tiến hành lưu vùng dữ liệu này với tên Category

  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/2e0f6e99-3de9-4f1e-b433-7987011f6aa2)

* Bảng Products:
  - Thực hiện các bước tương tự và tiến hành điền các giá trị Category_ID tương ứng sử dụng VLOOKUP, ta thu được kết quả sau:
  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/9c0c2db7-ba6f-48f4-a757-37af84cb8a9e)

 #### Tương tự với các bảng còn lại ta thu được kết quả sau 
* Bảng City:
* Bảng Region:
  - Sau khi tiến hành copy bảng, loại bỏ giá trị trùng lặp ta tạo Region_ID theo thứ tự R1,R2,... và thu được kết quả:
    
  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/f78dca49-d33b-4908-b7fc-d5e5ef324739)

  - Lưu vùng giá trị này với tên Region

* Bảng Country:
  - Ở bước tạo Country_ID, Tạo cột countryId, copy mã Alpha-code của các quốc gia từ trang web https://www.iban.com/countrycodes?fbclid=IwAR1gRAinFC-
_Bdm4dByKzHbUmz_8-qs-sv_Wjjd6xdsZakBbUi9iHcTCS5s vào Excel, và tiến hành VLOOKUP để có mã quốc gia tương ứng:

  ![image](https://github.com/sunday576/Globle_Super_Store_PJ/assets/156815133/15cd8b25-dcd0-4b07-af93-131d2df3f90e)

  - Vói một số quốc gia không có trong danh sách, ta sẽ tiến hành đặt mã thủ công sao cho không trùng lặp.
  - Kết quả thu được: 
* Bảng Customer:

  
## Data Visualization 
