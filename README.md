# HOTEL-BOOKING-SYSTEM
Made by DEBARGHYA CHOWDHURY(08) and SAMRAT MONDAL(03)
==================================================================================================
-- phpMyAdmin SQL Dump
-- version 5.0.3
-- https://www.phpmyadmin.net/
--

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- Database: `hotelbooking`
--

DELIMITER $$
--
-- Procedures
--
CREATE DEFINER=`root`@`localhost` PROCEDURE `CustData` (IN `CID` VARCHAR(5), IN `FNAME` VARCHAR(10), IN `LNAME` VARCHAR(10), IN `ADDR` VARCHAR(30), IN `PINCODE` DECIMAL(6,0), IN `DOB` DATE, IN `P_ID` VARCHAR(5))  begin
	DECLARE Counter varchar(4);
    	select count(CID) into Counter from CUSTOMER;
    	set counter = counter + 1;
    		IF length(PINCODE) <=> 6 THEN
    			INSERT into CUSTOMER VALUES (CID,FNAME,LNAME,ADDR,PINCODE,DOB,P_ID);
			SELECT 'YOUR DATA IS INSERTED' AS MESSAGE;
			ELSE
				SELECT 'Enter Valid Pincode' AS ERROR;
			END IF; 
END$$

CREATE DEFINER=`root`@`localhost` PROCEDURE `r1` (INOUT `Details` VARCHAR(1000))  BEGIN
	DECLARE bid1,fid1 TEXT;
    DECLARE exit_loop BOOLEAN DEFAULT FALSE;
    DECLARE bid_cursor CURSOR FOR SELECT BILL_ID,FID FROM bill;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET exit_loop=TRUE;
    OPEN bid_cursor;
    bid_loop: LOOP
    	FETCH FROM bid_cursor INTO bid1,fid1;
        IF exit_loop THEN
        	LEAVE bid_loop;
        END IF;
    	IF fid1='F01' THEN
    	SELECT bid1;
    	END IF;
    END LOOP bid_loop;
    CLOSE bid_cursor;
END$$

--
-- Functions
--
CREATE DEFINER=`root`@`localhost` FUNCTION `TOTAL_ROOMS` (`RCID` VARCHAR(5)) RETURNS INT(11) begin
			DECLARE no int;
 	select count(ROOM_NO) into no from ROOM R WHERE R.RCID=RCID;
			RETURN no;
end$$

DELIMITER ;

-- --------------------------------------------------------

--
-- Table structure for table `admin`
--

CREATE TABLE `admin` (
  `AID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `admin`
--

INSERT INTO `admin` (`AID`) VALUES
('A1');

-- --------------------------------------------------------

--
-- Table structure for table `bill`
--

CREATE TABLE `bill` (
  `BILL_ID` varchar(5) NOT NULL,
  `ROOM_NO` int(11) NOT NULL,
  `BILL_DATE` date NOT NULL,
  `CID` varchar(5) NOT NULL,
  `FID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `bill`
--

INSERT INTO `bill` (`BILL_ID`, `ROOM_NO`, `BILL_DATE`, `CID`, `FID`) VALUES
('B1', 101, '2019-04-10', 'C1', 'F1'),
('B2', 102, '2019-02-20', 'C2', 'F1'),
('B3', 103, '2019-05-01', 'C3', 'F3'),
('B4', 104, '2020-03-02', 'C4', 'F3'),
('B5', 105, '2018-08-10', 'C5', 'F6'),
('B6', 106, '2019-02-05', 'C6', 'F2'),
('B7', 107, '2019-04-10', 'C7', 'F7'),
('B8', 108, '2017-01-06', 'C8', 'F3'),
('B9', 109, '2015-04-10', 'C9', 'F5'),
('B10', 110, '2016-03-10', 'C10', 'F4'),
('B11', 111, '2019-09-03', 'C11', 'F3'),
('B12', 112, '2020-01-01', 'C12', 'F1'),
('B13', 113, '2019-10-02', 'C13', 'F2'),
('B14', 114, '2018-11-06', 'C14', 'F5'),
('B15', 115, '2018-12-30', 'C15', 'F3');

-- --------------------------------------------------------

--
-- Table structure for table `books`
--

CREATE TABLE `books` (
  `CHECKIN_DATE` date NOT NULL,
  `CHECKOUT_DATE` date NOT NULL,
  `CID` varchar(5) NOT NULL,
  `ROOM_NO` int(11) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `books`
--

INSERT INTO `books` (`CHECKIN_DATE`, `CHECKOUT_DATE`, `CID`, `ROOM_NO`) VALUES
('2019-01-12', '2019-01-16', 'C1', 101),
('2019-02-20', '2019-02-22', 'C2', 102),
('2019-05-01', '2019-05-06', 'C3', 103),
('2020-03-02', '2020-03-06', 'C04', 104),
('2018-08-10', '2018-08-12', 'C5', 105),
('2019-02-05', '2019-02-15', 'C6', 106),
('2019-04-10', '2019-04-15', 'C7', 107),
('2017-01-06', '2017-01-10', 'C8', 108),
('2015-04-10', '2015-04-15', 'C9', 109),
('2016-03-10', '2016-03-15', 'C10', 110),
('2019-09-03', '2019-09-06', 'C11', 111),
('2020-01-01', '2020-01-03', 'C12', 112),
('2019-10-02', '2019-10-06', 'C13', 113),
('2018-11-06', '2018-11-09', 'C14', 114),
('2018-12-30', '2019-01-01', 'C15', 115);

-- --------------------------------------------------------

--
-- Table structure for table `city`
--

CREATE TABLE `city` (
  `CITY` varchar(10) NOT NULL,
  `STATE` varchar(10) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `city`
--

INSERT INTO `city` (`CITY`, `STATE`) VALUES
('Bangalore', 'Karnataka'),
('Coimbatore', 'Tamil Nadu'),
('Delhi', 'Delhi'),
('Jaipur', 'Rajasthan'),
('Jamnagar', 'Gujarat'),
('Kolkata', 'West Benga'),
('Mumbai', 'Maharashtr'),
('Nadiad', 'Gujarat'),
('Pune', 'Maharashtr'),
('Rajkot', 'Gujarat'),
('Surat', 'Gujarat'),
('Udaipur', 'Rajasthan');

-- --------------------------------------------------------

--
-- Table structure for table `customer`
--

CREATE TABLE `customer` (
  `CID` varchar(5) NOT NULL,
  `FNAME` varchar(10) NOT NULL,
  `LNAME` varchar(10) NOT NULL,
  `ADDR` varchar(30) NOT NULL,
  `PINCODE` decimal(6,0) NOT NULL,
  `DOB` date NOT NULL,
  `P_ID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `customer`
--

INSERT INTO `customer` (`CID`, `FNAME`, `LNAME`, `ADDR`, `PINCODE`, `DOB`, `P_ID`) VALUES
('C1', 'Aanand', 'Pankhania', '26 - B, Timiliyawad Rd, Mehar ', '641009', '2000-04-22', 'P01'),
('C2', 'Prince', 'Nadpara', 'INS Hospital, near valentino b', '360005', '1998-02-28', 'P02'),
('C3', 'Vineet', 'Ghediya', '415,4th floor, infinity tower,', '110035', '1997-07-26', 'P03'),
('C4', 'Sapan', 'Kumar', '26 - B, Timiliyawad Rd, Mehar ', '400001', '1997-03-22', 'P04'),
('C5', 'Ram', 'Khunt', '305, Kashi Plaza Complex Opp, ', '641009', '2001-08-29', 'P05'),
('C6', 'Snehal', 'Malla', 'New Rander Rd, Giriraj Society', '700007', '2001-02-28', 'P06'),
('C7', 'Arka', 'Roy', '115-B, First floor, Zenon Besi', '110048', '1999-04-07', 'P07'),
('C8', 'Sam', 'Sosa', 'A-101, Maan Darwaja, Udhna dar', '395002', '1998-01-01', 'P08'),
('C9', 'Vernali', 'Sevak', 'M-59, second floor, Shreeji Ar', '387001', '1997-12-07', 'P09'),
('C10', 'Jeet', 'Patel', 'Apple Hospital, Udhna Dazwaja,', '395001', '2000-06-07', 'P10'),
('C11', 'Yash', 'Vora', 'Swami Narayan Complex, G-4 , 4', '176605', '2001-12-27', 'P11'),
('C12', 'Kumar', 'Pandya', '1st floor, sangini square, nea', '302011', '1973-08-16', 'P12'),
('C13', 'Shyamali', 'Joshi', 'Civil Char Rasta to Sosyo Circ', '560008', '1980-10-10', 'P13'),
('C14', 'Kapil', 'Dev', 'Behind Bhulka Bhavan School, A', '641009', '1990-09-29', 'P14'),
('C15', 'Urvashi', 'Joshi', 'House no. 6, First Floor New C', '176605', '2000-01-01', 'P15'),
('C16', 'Neha', 'Makvana', 'E-15, Rajiv Chowk, Block E, Co', '360001', '2000-12-12', 'P16');

-- --------------------------------------------------------

--
-- Table structure for table `customer_mobile_no`
--

CREATE TABLE `customer_mobile_no` (
  `MOBILE_NO` decimal(10,0) NOT NULL,
  `CID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `customer_mobile_no`
--

INSERT INTO `customer_mobile_no` (`MOBILE_NO`, `CID`) VALUES
('6731673654', 'C12'),
('7631571376', 'C8'),
('7813483746', 'C14'),
('7875468641', 'C3'),
('7954658465', 'C4'),
('8164835484', 'C13'),
('8316435464', 'C15'),
('8554879644', 'C5'),
('8724524527', 'C6'),
('8731734613', 'C11'),
('9137413641', 'C9'),
('9235146846', 'C6'),
('9298414734', 'C7'),
('9343873164', 'C11'),
('9475628582', 'C6'),
('9482515465', 'C1'),
('9685155131', 'C2'),
('9823853434', 'C10'),
('9851644854', 'C1'),
('9965846546', 'C4');

-- --------------------------------------------------------

--
-- Table structure for table `facilities`
--

CREATE TABLE `facilities` (
  `FID` varchar(5) NOT NULL,
  `FNAME` varchar(16) NOT NULL,
  `FAMOUNT` int(11) NOT NULL,
  `AID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `facilities`
--

INSERT INTO `facilities` (`FID`, `FNAME`, `FAMOUNT`, `AID`) VALUES
('F1', 'SPA', 5000, 'A1'),
('F2', 'SWIMMING POOL', 3000, 'A1'),
('F3', 'PARKING', 1000, 'A1'),
('F4', 'DANCE BAR', 4000, 'A1'),
('F5', 'TRANSPORTATION', 6000, 'A1'),
('F6', 'GAME ZONE', 1000, 'A1'),
('F7', 'BANQUET HALL', 5000, 'A1'),
('F8', 'Gym', 1050, 'A1');

-- --------------------------------------------------------

--
-- Table structure for table `logs`
--

CREATE TABLE `logs` (
  `ID` int(11) NOT NULL,
  `FID` varchar(3) NOT NULL,
  `Action` varchar(10) NOT NULL,
  `C_Date` datetime NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `logs`
--

INSERT INTO `logs` (`ID`, `FID`, `Action`, `C_Date`) VALUES
(1, 'F8', 'inserted', '2020-10-29 22:06:28');

-- --------------------------------------------------------

--
-- Table structure for table `payment`
--

CREATE TABLE `payment` (
  `P_ID` varchar(5) NOT NULL,
  `P_TYPE` varchar(15) NOT NULL,
  `BILL_ID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `payment`
--

INSERT INTO `payment` (`P_ID`, `P_TYPE`, `BILL_ID`) VALUES
('P1', 'CASH', 'B1'),
('P2', 'DEBIT CARD', 'B2'),
('P3', 'CREDIT CARD', 'B3'),
('P4', 'CASH', 'B4'),
('P5', 'CASH', 'B5'),
('P6', 'CREDIT CARD', 'B6'),
('P7', 'DEBIT CARD', 'B7'),
('P8', 'PAYTM', 'B8'),
('P9', 'CREDIT CARD', 'B9'),
('P10', 'PAYTM', 'B10'),
('P11', 'CASH', 'B11'),
('P12', 'CREDIT CARD', 'B12'),
('P13', 'DEBIT CARD', 'B13'),
('P14', 'CASH', 'B14'),
('P15', 'PAYTM', 'B15');

-- --------------------------------------------------------

--
-- Table structure for table `pincode`
--

CREATE TABLE `pincode` (
  `PINCODE` decimal(6,0) NOT NULL,
  `CITY` varchar(10) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `pincode`
--

INSERT INTO `pincode` (`PINCODE`, `CITY`) VALUES
('110035', 'Delhi'),
('110048', 'Delhi'),
('176605', 'Jamnagar'),
('302001', 'Jaipur'),
('302011', 'Jaipur'),
('302098', 'Udaipur'),
('322749', 'Pune'),
('360005', 'Rajkot'),
('360006', 'Rajkot'),
('360007', 'Rajkot'),
('387001', 'Nadiad'),
('395001', 'Surat'),
('395002', 'Surat'),
('400001', 'Mumbai'),
('400002', 'Mumbai'),
('400009', 'Mumbai'),
('560008', 'Bangalore'),
('641009', 'Coimbatore'),
('700007', 'Kolkata');

-- --------------------------------------------------------

--
-- Table structure for table `pricelog`
--

CREATE TABLE `pricelog` (
  `id` int(11) NOT NULL,
  `RCID` varchar(5) DEFAULT NULL,
  `RCNAME` varchar(10) DEFAULT NULL,
  `OldPrice` int(11) DEFAULT NULL,
  `NewPrice` int(11) DEFAULT NULL,
  `changedAt` timestamp NOT NULL DEFAULT current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `pricelog`
--

INSERT INTO `pricelog` (`id`, `RCID`, `RCNAME`, `OldPrice`, `NewPrice`, `changedAt`) VALUES
(1, 'R1', 'SINGLE', 2500, 1100, '2020-10-30 04:10:10');

-- --------------------------------------------------------

--
-- Table structure for table `rc_log`
--

CREATE TABLE `rc_log` (
  `id` int(11) NOT NULL,
  `RCID` varchar(5) NOT NULL,
  `RCNAME` varchar(10) NOT NULL,
  `changedate` datetime DEFAULT NULL,
  `action` varchar(50) DEFAULT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `rc_log`
--

INSERT INTO `rc_log` (`id`, `RCID`, `RCNAME`, `changedate`, `action`) VALUES
(1, 'R1', 'SINGLE', '2020-10-30 01:57:39', 'update'),
(2, 'R1', 'ONE_BED', '2020-10-30 02:31:31', 'update'),
(3, 'R1', 'SINGLE', '2020-10-30 09:26:27', 'update'),
(4, 'R1', 'SINGLE', '2020-10-30 09:34:36', 'update'),
(5, 'R1', 'SINGLE', '2020-10-30 09:37:58', 'update'),
(6, 'R1', 'SINGLE', '2020-10-30 09:40:10', 'update');

-- --------------------------------------------------------

--
-- Table structure for table `room`
--

CREATE TABLE `room` (
  `ROOM_NO` int(11) NOT NULL,
  `RCID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `room`
--

INSERT INTO `room` (`ROOM_NO`, `RCID`) VALUES
(101, 'R1'),
(102, 'R1'),
(103, 'R1'),
(115, 'R1'),
(104, 'R2'),
(110, 'R2'),
(108, 'R3'),
(112, 'R3'),
(103, 'R4'),
(111, 'R4'),
(109, 'R5'),
(105, 'R6'),
(106, 'R6'),
(107, 'R7'),
(114, 'R7');

-- --------------------------------------------------------

--
-- Table structure for table `room_catagory`
--

CREATE TABLE `room_catagory` (
  `RCNAME` varchar(10) NOT NULL,
  `RCID` varchar(5) NOT NULL,
  `MAX_GUESTS` decimal(2,0) NOT NULL,
  `TOTAL_ROOMS` int(11) NOT NULL,
  `ROOM_PRICE` int(11) NOT NULL,
  `DESCRIPTION` varchar(50) DEFAULT NULL,
  `AID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `room_catagory`
--

INSERT INTO `room_catagory` (`RCNAME`, `RCID`, `MAX_GUESTS`, `TOTAL_ROOMS`, `ROOM_PRICE`, `DESCRIPTION`, `AID`) VALUES
('SINGLE', 'R1', '1', 15, 1100, 'WHICH HAS SINGLE BED', 'A1'),
('TRIPLE', 'R2', '3', 10, 4000, 'THREE TWIN BEDS', 'A1'),
('QUAD', 'R3', '4', 10, 5500, 'MORE THAN TWO BEDS', 'A1'),
('QUEEN', 'R4', '2', 20, 8500, 'QUEEN SIZED BED', 'A1'),
('KING', 'R5', '2', 15, 10000, 'KING SIZED BED', 'A1'),
('TWIN', 'R6', '2', 10, 3000, 'TWO TWIN BEDS', 'A1'),
('DUPLEX', 'R7', '4', 10, 8000, 'TWO BEDS WITH TWO FLOORS', 'A1');

--
-- Triggers `room_catagory`
--
DELIMITER $$
CREATE TRIGGER `NEW_RC` BEFORE UPDATE ON `room_catagory` FOR EACH ROW BEGIN
		INSERT INTO rc_log
		SET action = 'update',
		RCID = OLD.RCID,
		RCNAME = OLD.RCNAME,
		changedate = NOW();
	END
$$
DELIMITER ;
DELIMITER $$
CREATE TRIGGER `PRICE_LOG` AFTER UPDATE ON `room_catagory` FOR EACH ROW BEGIN
        INSERT INTO Pricelog(RCID,RCNAME,OldPrice,NewPrice)
        VALUES(old.rcid, old.rcname, old.room_price, new.room_price);
END
$$
DELIMITER ;

-- --------------------------------------------------------

--
-- Table structure for table `uses`
--

CREATE TABLE `uses` (
  `CID` varchar(5) NOT NULL,
  `FID` varchar(5) NOT NULL
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;

--
-- Dumping data for table `uses`
--

INSERT INTO `uses` (`CID`, `FID`) VALUES
('C01', 'F1'),
('C1', 'F2'),
('C1', 'F5'),
('C2', 'F1'),
('C2', 'F3'),
('C3', 'F3'),
('C3', 'F6'),
('C4', 'F1'),
('C4', 'F3'),
('C4', 'F4'),
('C5', 'F3'),
('C5', 'F6'),
('C6', 'F3'),
('C7', 'F2'),
('C7', 'F3'),
('C8', 'F3'),
('C9', 'F2'),
('C9', 'F3'),
('C10', 'F1'),
('C10', 'F2'),
('C10', 'F5'),
('C11', 'F1'),
('C11', 'F6'),
('C12', 'F1'),
('C12', 'F3'),
('C13', 'F3'),
('C14', 'F3'),
('C14', 'F6'),
('C15', 'F3');

--
-- Indexes for dumped tables
--

--
-- Indexes for table `admin`
--
ALTER TABLE `admin`
  ADD PRIMARY KEY (`AID`);

--
-- Indexes for table `bill`
--
ALTER TABLE `bill`
  ADD PRIMARY KEY (`BILL_ID`),
  ADD KEY `CID` (`CID`),
  ADD KEY `FID` (`FID`);

--
-- Indexes for table `books`
--
ALTER TABLE `books`
  ADD PRIMARY KEY (`CHECKIN_DATE`),
  ADD UNIQUE KEY `ROOM_NO` (`ROOM_NO`,`CID`,`CHECKIN_DATE`,`CHECKOUT_DATE`),
  ADD KEY `CID` (`CID`);

--
-- Indexes for table `city`
--
ALTER TABLE `city`
  ADD PRIMARY KEY (`CITY`);

--
-- Indexes for table `customer`
--
ALTER TABLE `customer`
  ADD PRIMARY KEY (`CID`),
  ADD KEY `P_ID` (`P_ID`);

--
-- Indexes for table `customer_mobile_no`
--
ALTER TABLE `customer_mobile_no`
  ADD PRIMARY KEY (`MOBILE_NO`,`CID`),
  ADD KEY `CID` (`CID`);

--
-- Indexes for table `facilities`
--
ALTER TABLE `facilities`
  ADD PRIMARY KEY (`FID`),
  ADD KEY `AID` (`AID`);

--
-- Indexes for table `logs`
--
ALTER TABLE `logs`
  ADD PRIMARY KEY (`ID`);

--
-- Indexes for table `payment`
--
ALTER TABLE `payment`
  ADD PRIMARY KEY (`P_ID`),
  ADD KEY `BILL_ID` (`BILL_ID`);

--
-- Indexes for table `pincode`
--
ALTER TABLE `pincode`
  ADD PRIMARY KEY (`PINCODE`);

--
-- Indexes for table `pricelog`
--
ALTER TABLE `pricelog`
  ADD PRIMARY KEY (`id`);

--
-- Indexes for table `rc_log`
--
ALTER TABLE `rc_log`
  ADD PRIMARY KEY (`id`);

--
-- Indexes for table `room`
--
ALTER TABLE `room`
  ADD PRIMARY KEY (`ROOM_NO`),
  ADD KEY `RCID` (`RCID`);

--
-- Indexes for table `room_catagory`
--
ALTER TABLE `room_catagory`
  ADD PRIMARY KEY (`RCID`),
  ADD KEY `AID` (`AID`);

--
-- Indexes for table `uses`
--
ALTER TABLE `uses`
  ADD PRIMARY KEY (`CID`,`FID`),
  ADD KEY `FID` (`FID`);

--
-- AUTO_INCREMENT for dumped tables
--

--
-- AUTO_INCREMENT for table `logs`
--
ALTER TABLE `logs`
  MODIFY `ID` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT for table `pricelog`
--
ALTER TABLE `pricelog`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=2;

--
-- AUTO_INCREMENT for table `rc_log`
--
ALTER TABLE `rc_log`
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=7;

--
-- Constraints for dumped tables
--

--
-- Constraints for table `bill`
--
ALTER TABLE `bill`
  ADD CONSTRAINT `bill_ibfk_1` FOREIGN KEY (`CID`) REFERENCES `customer` (`CID`),
  ADD CONSTRAINT `bill_ibfk_2` FOREIGN KEY (`FID`) REFERENCES `facilities` (`FID`);

--
-- Constraints for table `books`
--
ALTER TABLE `books`
  ADD CONSTRAINT `books_ibfk_1` FOREIGN KEY (`CID`) REFERENCES `customer` (`CID`),
  ADD CONSTRAINT `books_ibfk_2` FOREIGN KEY (`ROOM_NO`) REFERENCES `room` (`ROOM_NO`);

--
-- Constraints for table `customer_mobile_no`
--
ALTER TABLE `customer_mobile_no`
  ADD CONSTRAINT `customer_mobile_no_ibfk_1` FOREIGN KEY (`CID`) REFERENCES `customer` (`CID`);

--
-- Constraints for table `payment`
--
ALTER TABLE `payment`
  ADD CONSTRAINT `payment_ibfk_1` FOREIGN KEY (`BILL_ID`) REFERENCES `bill` (`BILL_ID`);

--
-- Constraints for table `room`
--
ALTER TABLE `room`
  ADD CONSTRAINT `room_ibfk_1` FOREIGN KEY (`RCID`) REFERENCES `room_catagory` (`RCID`);

--
-- Constraints for table `uses`
--
ALTER TABLE `uses`
  ADD CONSTRAINT `uses_ibfk_1` FOREIGN KEY (`CID`) REFERENCES `customer` (`CID`),
  ADD CONSTRAINT `uses_ibfk_2` FOREIGN KEY (`FID`) REFERENCES `facilities` (`FID`);
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
