---
title: Wargames - Bandit
published: 2026-01-02
description: Làm quen Linux
category: OverTheWire
tags: [Wargames, Linux]
draft: false
image: ./images/avtbandit.jpg
---

## Bandit0
> - User: bandit0
> - Pass: bandit0

Kết nối đến máy chủ Bandit thông qua giao thức SSH với địa chỉ bandit.labs.overthewire.org và cổng 2220.

`ssh` - giao thức cho phép người dùng điều khiển và làm việc với máy chủ từ xa an toàn.
```bash
#ssh user@host -p port 
ssh bandit0@bandit.labs.overthewire.org -p 2220 
```

## Bandit1
> - User: bandit1
> - Pass: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If


`ls` – lệnh dùng để liệt kê các file và thư mục trong thư mục hiện tại (không bao gồm các file ẩn).

`cat` – lệnh dùng để hiển thị nội dung của file ra màn hình. 
```bash
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme 
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Bandit2
> - User: bandit2
> - Pass: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx 

`file` – lệnh dùng để xác định kiểu dữ liệu thực sự của một file, không phụ 
thuộc vào tên hay phần mở rộng. 

Trong level 2 này, file cần đọc có tên là `./-`. Ký hiệu `./` đây là đường dẫn 
tương đối, chỉ file nằm trong thư mục hiện tại. 

- Phân biệt đường dẫn: 
    - Đường dẫn tuyệt đối – bắt đầu từ thư mục gốc `/` và chỉ rõ toàn bộ đường 
đi đến file. 
    - Đường dẫn tuơng đối – được xác định dựa trên thư mục đang đứng, ký 
hiệu `.`
```bash
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ file ./-
./-: ASCII text
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## Bandit3
> - User: bandit3
> - Pass: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx 

- Ở level 3 này, tên file có chứa khoảng trống. Khi thao tác với file, cần sử 
dụng ký tự `\` trước khoảng trống để hệ thống hiểu đúng tên file và thực thi lệnh chính xác. 
```bash
bandit2@bandit:~$ ls
--spaces in this filename--
bandit2@bandit:~$ file ./--spaces\ in\ this\ filename-- 
./--spaces in this filename--: ASCII text
bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename-- 
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## Bandit4
> - User: bandit4
> - Pass: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

`cd` - lệnh dùng để di chuyển vào thư mục mong muốn. 

Trong level 4 này, file chứa mật khẩu nằm trong thư mục con và là file ẩn. 
Vì vậy, cần sử dụng thêm tùy chọn của lệnh `ls` để liệt kê đầy đủ các file trong thư 
mục. 

Cú pháp: `ls [tùy chọn]`

`ls -la` – iệt kê toàn bộ file và thư mục, bao gồm cả file ẩn và thông tin 
quyền truy cập.
```bash
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere/
bandit3@bandit:~/inhere$ ls -la
total 12
drwxr-xr-x 2 root    root    4096 Oct 14 09:26 .
drwxr-xr-x 3 root    root    4096 Oct 14 09:26 ..
-rw-r----- 1 bandit4 bandit3   33 Oct 14 09:26 ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ./...Hiding-From-You 
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Bandit5
> - User: bandit5
> - Pass: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

Trong level 5 này, thư mục chứa nhiều file khác nhau. Để xác định file chứa 
mật khẩu, em sử dụng ký tự đại diện `*` kết hợp với đường dẫn tương đối để kiểm tra đồng thời các file trong thư mục. 

`*` – ký tự đại diện cho tất cả các file trong thư mục hiện tại.
```bash
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## Bandit6
> - User: bandit6
> - Pass: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

Trong level 6 này, yêu cầu tìm file chứa mật khẩu thỏa mãn các điều kiện: 
có quyền đọc, kích thước 1033 byte và không có quyền thực thi. Để tìm file thỏa mãn các điều kiện trên, sử dụng lệnh `find`.  

`find` – lệnh dùng để tìm kiếm thư mục hay file dựa theo điều kiện. 

`.` – thư mục hiện tại 

`-type f` – tìm các file thường -size 1033c – file có kích thước 1033 byte 

`-readable` - có quyền đọc

`! -executable` – file không có quyền thực thi 
```bash
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
bandit5@bandit:~/inhere$ find . -type f -readable -size 1033c ! -executable 
./maybehere07/.file2
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Bandit7
> - User: bandit7
> - Pass: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

Trong level này, yêu cầu tìm file chứa mật khẩu thỏa mãn các điều kiện: 
thuộc user bandit7, thuộc group bandit6 và có kích thước 33 byte. Để tìm file thỏa mãn các điều kiện trên, sử dụng lệnh `find.`

`/` – thư mục gốc, cho phép tìm kiếm trên toàn bộ hệ thống.  

`-user bandit7` – file thuộc sở hữu của user bandit7 

`-group bandit6` – file thuộc group bandit6 
 
`2>/dev/null` – ẩn các thông báo lỗi do không có quyền truy cập khi 
tìm kiếm từ thư mục gốc. => `2>/dev/null` dùng để chuyển stderr (standard error) vào /dev/null. Khi tìm kiếm từ thư mục gốc `/`, hệ thống sẽ sinh ra nhiều thông báo lỗi do không có quyền truy cập vào một số thư mục. Việc chuyển stderr vào /dev/null giúp ẩn các thông báo lỗi này, tránh làm rối màn hình, trong khi kết quả tìm kiếm hợp lệ vẫn được hiển thị. (nó còn hay gọi là hố đen).
```bash
bandit6@bandit:~$ find / -type f -size 33c -user bandit7 -group bandit6 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

## Bandit8 
> - User: bandit8
> - Pass: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

Level 8, yêu cầu tìm chuỗi millionth trong file data.txt

`grep` – lệnh dùng để tìm kiếm một chuỗi ký tự trong nội dung của file, khác với lệnh find là tìm file theo điều kiện.
```bash
bandit7@bandit:~$ grep "millionth" data.txt
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```

## Bandit9
> - User: bandit9
> - Pass: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM 

`sort` – sắp xếp các dòng của file 

`|` – dùng để kết hợp nhiều lệnh 

`uniq` – loại bỏ các dòng trùng lặp 

`-u` – chỉ hiển thị các dòng xuất hiện đúng một lần (-u là tùy chọn của uniq) 
```bash
bandit8@bandit:~$ sort data.txt | uniq -u
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```

## Bandit10
> - User: bandit10
> - Pass: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

`strings` – lệnh dùng để trích xuất và hiển thị các chuỗi ký tự có thể đọc được từ file, thường được sử dụng với các file nhị phân.
```bash
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ strings data.txt | grep ====
========== the
========== password
f\Z'========== is
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
```

## Bandit11
> - User: bandit11
> - Pass: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
- Sau khi kiểm tra, đề bài cho file đã bị mã hóa(Encode) Base64.  
- Dấu hiệu nhận biết Base64: `A–Z a–z 0–9 + /` và có thể kết thúc chuỗi bảng `=` hoặc `==` (padding)
`base64 -d` - lệnh dùng để giải mã (Decode) Base64
```bash
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt
VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTR3NnMlJXbnBOVmozcVJyCg==
bandit10@bandit:~$ base64 -d data.txt
The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
