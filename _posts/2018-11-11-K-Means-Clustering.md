---
title: K-Means Clustering
tags: Machine Learning
---

# K-Means Clustering

![K-Means Clustering](https://media1.giphy.com/media/12vVAGkaqHUqCQ/source.gif)
## Tổng quan
* Mục đích: tìm một cách phân nhóm tốt nhất các cá thể thành 1 số lớp định trước (các lớp này rời nhau)
* Xác định k nhóm (k là số được chọn trước) từ n cá thể dựa vào thuật toán lặp (định vị tâm) nhắm tối ưu hóa một tiêu chuẩn đo lường phân cụm
* Thuật toán cơ sở
   1. Chọn ngẫu nhiên k điểm làm tâm của k cụm (Initialization step)
   2. **repeat**: 
   
      1. Tạo k cụm bằng cách xếp mỗi cá thể vào cụm có tâm gần nó nhất (Assignment step)
   
      2. Xác định tâm mới của mỗi cụm bằng cách **tính trung bình** (Update Step)
   3. **until**: các tâm cụm không thay đổi

![K-Means](http://www.datamilk.com/kmeans_animation.gif)

* Đặc điểm:

   * K-Means thuộc loại thuật toán học không giám sát (Unsupervised)
   * Do các điểm trung tâm ban đầu khởi tạo và ngẫu nhiên nên kết quả các lần chạy có thể khác nhau
   * Kết quả của giải thuậ phụ thuộc rất nhiều vào vị trí khởi tạo của các điểm trung tâm (centroid) ban đầu
   * Độ phức tạp O(n ∗ k ∗ I ∗ d), n là số điểm (cá thể), k là số cụm, I là số bước lặp, d là số chiều dữ liệu (số thuộc tính)
   * Độ đo khoảng cách có thể là khoảng cách Euclid, độ tương tự cosin, độ tương quan ...
   
* Hạn chế: 
   * Cần biết trước số lượng cluster
   * Nghiệm cuối cùng phụ thuộc vào số lượng cluster ban đầu
   * Các cluster cần có số lượng điểm bằng nhau
   * Các cluster cần có dạng hình tròn
   * Khi một cluster nằm trong một cluster khác thì thuật toán đưa kết quả không mong muốn
   * Ảnh hưởng bỏi ngoại lệ lớn
   * Phân nhóm cluster bị ảnh hưởng bởi mật độ cụm
   
* Random k-means initialization và Forgy k-means initialization
  * Forgy: Initialization -> Assignment -> Update
  * Random: Initialization -> Update -> Assignment
  
* Vấn đề khởi tạo các tâm cụm
  * Số cách chọn tâm cụm ngẫu nhiên là rất lớn, cách chọn tâm cụm ban đầu đóng vai trò quan trọng, ảnh hưởng tới kết quả
  * Một số giải pháp:
    * Chạy nhiều lần (tuy nhiên không thể thử hết mọi cách chạy)
    * Lấy mẫu và dùng phương pháp phân cấp để xác định các tâm khởi tạo
    * Chọn nhiều hơn k tâm rồi lựa chọn thu gọn k tâm tách biệt
    * Phân cụm với số cụm lớn rồi thực hiện phân cụm phân cấp

* Reference
    * Machine Learning cơ bản
    * Atrifical Intelligence for Humans Vol 1: Fundamental 
