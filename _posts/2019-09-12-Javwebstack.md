---
title: Java Web Development Stack
tags: Java, Web-development, Back-end
---

@Author: damminhtien

@LastUpdate: 21/10/2019

## 1. Java Servlet:
Servlet có thể được mô tả bằng nhiều cách, tùy thuộc vào ngữ cảnh:
* Servlet là một công nghệ được sử dụng để tạo ra ứng dụng web.
* Servlet là một API cung cấp các interface và lớp bao gồm các tài liệu.
* Servlet là một thành phần web được triển khai trên máy chủ để tạo ra trang web động.

Có nhiều interface và các lớp trong API servlet như Servlet, GenericServlet, HttpServlet, ServletRequest, ServletResponse,...

Java Servlet là core của nhiều Java Web Framework như Spring, Struts,...

Servlet life cycle:

![Servlet life cycle](https://o7planning.org/vi/10169/cache/images/i/12877.png)

Đây là các nguyên tắc mà bạn nên nhớ để có thể xây dựng một ứng dụng Web sử dụng Servlet + JSP thỏa mãn tiêu chí: code đơn giản dễ hiểu và dễ dàng bảo trì.

Các nguyên tắc:
1. Đừng bao giờ cho phép người dùng truy cập trực tiếp vào trang JSP của bạn.
2. Chỉ coi JSP là cái để hiển thị giao diện.
3. Servlet đóng vai trò là người điều khiển luồng đi của ứng dụng và sử lý logic chương trình.
4. Mở kết nối JDBC và quản lý giao dịch trong Filter (Không bắt buộc).

## 2. Java Servlet Filter == Middleware
## 3. JSP == Java Server Page
Là công nghệ View của Java.

## 4. JDBC 
JDBC (Java Database Connectivity) là một API tiêu chuẩn dùng để tương tác với các loại cơ sở dữ liệu quan hệ.
JDBC có một tập hợp các class và các Interface dùng cho ứng dụng Java có thể nói chuyện với các cơ sở dữ liệu.

![JDBC](https://o7planning.org/vi/10167/cache/images/i/1007105.jpeg)

## 5. Java Spring:
