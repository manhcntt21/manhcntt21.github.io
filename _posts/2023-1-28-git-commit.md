---
title: Git commit phần 1: Chỉnh sửa commit
categories:
  - git
  - git-basic
  - git-commit
  - self-learning
---
Về ý nghĩa nó chỉ đơn giản là chúng ta tổng hợp tất cả những file đã tạo và thay đổi thành một việc có ý nghĩa và đặt tên cái việc đó thành message của commit. Nhưng ở đây tôi không tập chung vào syntax thông dụng, cái tôi hướng tới là các use case của nó.

* Vấn đề:

Đa phần chúng ta khi mới dùng git thường chạy các lệnh cơ bản của git như: git add, git commit, git push,...

Chúng ta có thể add và commit tất cả nhưng file mà chúng ta muốn một cách lặp đi lặp lại, điều này dẫn tới một thực tế là ở một thời điểm nào đó chúng ta chợt nhớ ra mình đã quên một số file ở commit vừa mới thực hiện (nghĩa là chưa đẩy lên remote repository, mới chỉ commit thôi!) cần được thêm vào commit đó (hay gọi là stage chúng). 

Những file này có thể là **unstracked** (git chưa biết) hoặc là ở trạng thái **modified** (bổ sung thêm một vài chỉnh sửa của file mà nó đã được git track trong commit vừa rồi)

* Giải pháp:

Một cách thông thường chúng ta hoàn toàn có thể thực hiện một commit mới để bổ sung điều đó, sau đó nếu cần thiết có thể dùng **git rebase** để merge commit hoặc có thể dùng **git reset --hard** or **git reset --mixed** ngay từ đầu. (Mình sẽ bàn chi tiết về 2 câu lệnh này vào một dịp khác, các bạn có thể tham khảo bài viết [này](Git-Branching-Rebasing) nếu muốn)

Nhưng mình muốn hướng tới một giải pháp ngắn gọn và đơn giản, đễ hiểu hơn để giải quyết, đó là dùng **git commit --amend**.

Bản thân **git commit** có rất nhiều tham số, mình chưa có điều kiện để dùng. Nhưng khi vô tình tìm được **--amend**, mình đã thầm cảm ơn ông trời rất nhiều. 


Tại thời điểm bạn nhận ra mình cần thực hiện bổ sung:

Nếu là file đã được git staging, bạn tiến hành chỉnh sửa, thêm bớt, ... và thực hiện git add để staging các thay đổi đó, cuối cùng là dùng **git commit --amend**, một trình soạn thảo (dùng các quy tác của vim editor) để thay đổi message của commit

Nếu là unstracked file, thì việc làm của chúng ta đơn giản hơn nhiều, chỉ cần git add và sau đó **git commit --amend** là xong

* Kết luận

Một điều lưu ý là commit hash sẽ thay đổi dù có dùng bất kể cách nào trong 3 cách mình có nêu ở trên, điều này là quan trọng với những pulic branch, commit (Đây là một vấn đề rất quan trọng mình sẽ nói về nó vào một thời điểm khác).

Một trích dẫn của git book về [Git-Branching-Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing#_rebase_peril) dành cho những ai rebase shared branch, khi mình đọc mình cũng phải bật cười.
> "If you follow that guideline, you’ll be fine. If you don’t, people will hate you, and you’ll be scorned by friends and family."

Còn về ví dụ, mình thấy chưa có gì nhiều về mặt logic, nó khá đơn giản, mình sẽ bổ sung sau. See you late, thank you for reading.

