---
title: Git commit phần 2: Xoá một commit
categories:
  - git
  - git-basic
  - git-commit
  - self-learning
---

Thời gian vừa qua mình tương đối bận rộn vì phải dành thời gian cho một số công việc cá nhân. Mình xin các bạn thứ lỗi.

Tiếp tục series về git commit, hôm nay mình sẽ cũng các bạn thảo luận về xoá một commit. Mình thường tiếp cận từ các use case thực tế để học một thứ gì đó và việc xoá một commit cũng vậy.

* Vấn đề:

Với xoá một commit, chúng ta sẽ chia làm hai vấn đề nhỏ như sau:

1 Xoá commit đã đẩy lên remote repository

2 Xoá commit ở local repository

* Thông tin bổ sung

Vì khi xoá một commit chúng ta có thể kiểm soát được trạng thái của file sau khi xoá commit nên mình sẽ tóm tát về trạng thái của file một chút ở đây để mọi người ôn lại cũng như tổng kết một chút kiến thức ở [phần 1](2023-1-28-git-commit.md).

Chúng ta đã biết git quản lý một file (hoặc nhiều file, ở đây mình nêu vấn đề với một file cho đơn giản) với 2 trạng thái

a. tracked file: mọi người xem chi tiết ở phần dưới.

b. unstracked file: đây là trạng thái khi ta thêm một file vào git mà git không hề biết gì về sự tồn tại của nó. Như ví dụ ở Hình 1.

![unstracked file in git](/assets/images/2023-03-25/unstracked-file.png)

<center>Hình 1: Ví dụ về unstracked file</center>


Với trạng thái tracked file lại chia thành 3 trạng thái nhỏ nữa:

a1. modified: một file đã git track thông qua hoạt động commit trong quá khứ, sau đó bị chỉnh sửa sẽ có trạng thái này

![modified](/assets/images/2023-03-25/modified.png)

<center>Hình 2: Ví dụ về modified file</center>

a2. staging: đây là trạng thái mà các file được chuẩn bị để cho lần commit tiếp theo, thông qua lệnh **git add**, cụ thể hơn từ trạng thái modified hoặc unstracked sẽ đến staging thông qua git add

![staging](/assets/images/2023-03-25/staging.png)

<center>Hình 3: Ví dụ về staging</center>

a3. commited: đây là trạng thái mà các thay đổi được lưu vào một khái niệm gọi là snapshot, hay hiểu đơn giản là khi chúng ta thực hiện **git commit**

![committed](/assets/images/2023-03-25/committed.png)

<center>Hình 4: Ví dụ về committed</center>

* Giải pháp

Từ việc xác đinh trạng thái của file như mình đã trình bày ở phần thông tin bổ sung, hôm nay mình sẽ hướng dẫn các bạn sử dụng **git reset** một cách hiệu quả để đạt được những điều các bạn muốn. Sẽ tồn tại 3 cách như sau.

Đầu tiên là chúng ta muốn file của chúng ta ở trạng thái *committed*, có thể hiểu là nó trở về trạng thái của commit trước và chúng ta sẽ mất mọi thứ.

Để cho các bạn dễ hình dung, mình sẽ tóm tắt kịch bản được thể hiện dưới ảnh như sau: Chúng ta đang ở trên nhánh delete-commit1, commit mới nhất có message là add baby lyrics chỉ chứ duy nhất một file baby.txt.

![reset-hard-before](/assets/images/2023-03-25/reset-hard-before.png)

<center>Hình 5: Trước khi thực hiện git reset hard</center>

Điều quan trọng ở đây là cần xác định commit mà bạn buốn quay lại, mình thường dùng **git log --oneline để xác định**. Giả sử mình muốn quay lại commit ngay trước đó.

Mình thực hiện **git reset --hard 659e5e0**

![reset-hard-after](/assets/images/2023-03-25/reset-hard-after.png)

<center>Hình 6: Sau khi thực hiện git reset hard</center>

Như kết quả, các bạn thấy file đã hoàn toàn biến mất khỏi thư mục của mình, có thể coi là nó chưa từng tồn tại. 

Nhưng một điều lưu ý các bạn có thể mở rộng vấn đề để tự trả lời, liệu git có thực sự xoá code của chúng ta không? nếu không thì nó gọi là cái gì và chúng ta có thể làm thế nào để lấy lại? Mình sẽ trả lời vào một thời điểm khác để tránh bài dài.

Thứ hai, chúng ta muốn quay trở về commit trước nhưng không xoá mọi thứ đi như cách 1 và muốn file của chúng ta ở trạng thái staging (tình huống thức tế có thể là: sau khi commit xong, chúng ta nhớ ra cần phải add thêm file vào commit cho đúng logic)

![reset-soft-after](/assets/images/2023-03-25/reset-soft-after.png)

<center>Hình 7: Sau khi thực hiện git reset soft</center>

Như kết quả các bạn thấy, commit đã biến mất, file vẫn còn và đang ở trạng thái staging, bạn hoàn toàn có thể thêm bất kì logic mới nào để thực hiện commit tiếp theo.

Cách cuối cùng, sử dụng git reset không tham số hoặc --mixed, trường hợp này thì commit bị xoá và file được đưa về trạng thái unstracked.

![reset-mixed-after](/assets/images/2023-03-25/reset-mixed-after.png)

<center>Hình 8: Sau khi thực hiện git reset không tham số hoặc --mixed</center>

* Tổng kết

Như vậy mình đã trình bay về các trạng thái của file cũng như cách sử dụng thông thường của git reset liên quan đến các trạng thái này. Tuỳ thuộc vào nhu cầu của các bạn, các bạn có thể chọn phương thức phù hợp.

git reset --hard (commit-hard)

git reset --soft (commit-hard)

git reset --mixed (commit-hard) or git reset (commit-hard)

* Cuối cùng

Mình viết bài này hoàn toàn là vì cộng đồng, nhưng nếu các bạn thấy hay, có ích mà muốn donate cho mình, mình rất cảm ơn, cũng như là một nguồn động lực to lớn để mình ra được các bài viết chất lượng hơn.

Buy me a coffee
![Buy me a coffee](/assets/images/coffe.jpg)