CREATE DATABASE IF NOT EXISTS QuanLyBanHang CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE QuanLyBanHang;

-- 1. Tạo bảng Customer
CREATE TABLE Customer (
    cID INT AUTO_INCREMENT PRIMARY KEY,
    cName VARCHAR(50) NOT NULL,
    cAge TINYINT
);

-- 2. Tạo bảng Order
CREATE TABLE `Order` (
    oID INT AUTO_INCREMENT PRIMARY KEY,
    cID INT NOT NULL,
    oDate DATETIME NOT NULL,
    oTotalPrice INT DEFAULT NULL,
    CONSTRAINT fk_order_customer FOREIGN KEY (cID) REFERENCES Customer(cID)
);

-- 3. Tạo bảng Product
CREATE TABLE Product (
    pID INT AUTO_INCREMENT PRIMARY KEY,
    pName VARCHAR(50) NOT NULL,
    pPrice INT NOT NULL
);

-- 4. Tạo bảng OrderDetail
CREATE TABLE OrderDetail (
    oID INT NOT NULL,
    pID INT NOT NULL,
    odQTY INT NOT NULL,
    PRIMARY KEY (oID, pID),
    CONSTRAINT fk_orderdetail_order FOREIGN KEY (oID) REFERENCES `Order`(oID),
    CONSTRAINT fk_orderdetail_product FOREIGN KEY (pID) REFERENCES Product(pID)
);

-- 5. Chèn dữ liệu mẫu
INSERT INTO Customer (cName, cAge) VALUES
('Minh Quan', 10),
('Ngoc Oanh', 20),
('Hong Ha', 50);

INSERT INTO Product (pName, pPrice) VALUES
('May Giat', 3),
('Tu Lanh', 5),
('Dieu Hoa', 7),
('Quat', 1),
('Bep Dien', 2);

INSERT INTO `Order` (cID, oDate, oTotalPrice) VALUES
(1, '2006-03-21', NULL),
(2, '2006-03-23', NULL),
(1, '2006-03-16', NULL);

INSERT INTO OrderDetail (oID, pID, odQTY) VALUES
(1, 1, 3),
(1, 3, 7),
(1, 4, 2),
(2, 1, 1),
(3, 1, 8),
(2, 5, 4),
(2, 3, 3);
