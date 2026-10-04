# Bài 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Mục tiêu

* Sử dụng `.gitignore` để bỏ qua các file nhạy cảm.
* Gỡ file `credentials.txt` khỏi Git tracking nhưng không xóa file vật lý trên máy.
* Sử dụng `git commit --amend` để sửa thông điệp của commit gần nhất.
* Kiểm tra trạng thái Git và lịch sử commit.

---

## 2. Bối cảnh

Trong quá trình làm bài, file `credentials.txt` chứa thông tin nhạy cảm đã bị commit nhầm vào Git.

Yêu cầu xử lý:

1. Giữ lại file `credentials.txt` trên máy.
2. Gỡ file `credentials.txt` khỏi Git tracking.
3. Thêm `credentials.txt` vào `.gitignore` để Git bỏ qua file này trong tương lai.
4. Sửa thông điệp của commit gần nhất bằng `git commit --amend`.

---

## 3. Nội dung file .gitignore

File `.gitignore` được tạo với nội dung:

```gitignore
# Sensitive files
credentials.txt

# Environment files
.env
.env.*

# System files
.DS_Store
Thumbs.db

# IDE files
.idea/
.vscode/
```

Trong đó:

```text
credentials.txt
```

được sử dụng để yêu cầu Git bỏ qua file chứa thông tin nhạy cảm.

---

## 4. Gỡ credentials.txt khỏi Git tracking

Ban đầu, `credentials.txt` đã được commit vào repository.

Sử dụng lệnh:

```bash
git rm --cached credentials.txt
```

Lệnh trên chỉ xóa file khỏi Git index/cache theo dõi, không xóa file vật lý khỏi thư mục làm việc.

Sau đó kiểm tra file vẫn tồn tại:

```bash
Get-Content credentials.txt
```

Kết quả:

```text
username=demo_user
password=demo_password
api_key=demo_api_key
```

Điều này chứng minh file `credentials.txt` vẫn tồn tại trên máy.

---

## 5. Commit thay đổi

Thêm `.gitignore` vào staging:

```bash
git add .gitignore
```

Sau đó commit:

```bash
git commit -m "Ignore credentials file"
```

---

## 6. Sửa commit bằng --amend

Sử dụng:

```bash
git commit --amend -m "Remove credentials tracking and update gitignore"
```

Lệnh `--amend` được sử dụng để thay đổi commit gần nhất thay vì tạo thêm một commit mới.

---

## 7. Kiểm tra trạng thái Git

Sử dụng:

```bash
git status
```

Kết quả mong đợi:

```text
On branch ...
nothing to commit, working tree clean
```

File `credentials.txt` không còn xuất hiện dưới dạng Staged hoặc Modified.

---

## 8. Kiểm tra lịch sử commit

Sử dụng:

```bash
git log -n 1
```

Kết quả:

```text
commit <commit-id>
Author: <your-name>
Date:   <date>

    Remove credentials tracking and update gitignore
```

Thông điệp commit gần nhất đã được sửa thành công bằng `--amend`.

---

## 9. Kiểm tra credentials.txt không còn được Git tracking

Sử dụng:

```bash
git ls-files credentials.txt
```

Kết quả không hiển thị `credentials.txt`.

Điều này chứng minh file đã được gỡ khỏi Git tracking.

Tuy nhiên, file vẫn tồn tại trong thư mục làm việc cục bộ.

---

## 10. Kết luận

Đã hoàn thành các yêu cầu của bài:

* Tạo và cấu hình `.gitignore`.
* Thêm `credentials.txt` vào danh sách file bị Git bỏ qua.
* Sử dụng `git rm --cached credentials.txt` để gỡ file khỏi Git tracking.
* Không xóa file vật lý khỏi máy.
* Sử dụng `git commit --amend` để sửa thông điệp commit gần nhất.
* Kiểm tra trạng thái bằng `git status`.
* Kiểm tra lịch sử bằng `git log -n 1`.
