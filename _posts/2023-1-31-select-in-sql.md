---
title: Những điều hay ho về SELECT mà ít người để ý phần 1
categories:
  - sql
  - sql-basic
---

Hôm nay, chúng mình sẽ bàn về SELECT với ALIASES. 
* Vấn đề như sau
```sql
select 
	productid	as id,
	productname as name
from
	products
where
    id = 1
```
Không ít lần trong đời, chúng ta đã tùng dùng tên đã đổi ở SELECT để dùng lại ở mệnh đề WHERE và rất tiếc các RDBMS đều phản hồi lại **invalid name 'id'**

* Giải thích:

Lỗi như vậy là do chúng ta chưa quan tâm đến thứ tự logic của câu lệnh SELECT, các bạn có thể tham khảo ở [Logical Processing Order of the SELECT statement](https://learn.microsoft.com/en-us/sql/t-sql/queries/select-transact-sql?view=sql-server-ver16). Quay lại vấn đề ban đầu, lỗi như vậy là do, trên thực thế, khi thực thi câu lệnh sql thì thứ tự là FROM > WHERE > SELECT, như vậy là do tại WHERE thì câu lệnh đổi tên chưa được thực thi nên báo lỗi.

* Giải pháp:

Nhưng nếu chúng ta vẫn muốn đạt được mục đích tham chiếu đến alias name đó thì sao? Đó là lúc chúng ta cần đến một cái gọi là INLINE VIEW.
```
select
	*
from 
	(
		select
			productid	as id,
			productname as name
		from 
			products
	) x
where
	x.id between 1 and 10
-- x hoặc x.id đều được
```
Biến x ở trên tuỳ thuộc vào từng RDBMS mà có bắt buộc hay không, nếu bạn dùng SQL Server thì bắt buộc phải có, nó là tên của INLINE VIEW. Nó chạy được là do theo thứ tự đã nói ở trên FROM > WHERE, nên ở WHERE nó hiểu và quá trình thực thi câu lệnh chắc chắn thành công.

* Cuối cùng

Mình viết bài này hoàn toàn là vì cộng đồng, nhưng nếu các bạn thấy hay, có ích mà muốn donate cho mình, mình rất cảm ơn, cũng như là một nguồn động lực to lớn để mình ra được các bài viết chất lượng hơn.

Buy me a coffee

![Buy me a coffee](/assets/images/coffe.jpg)