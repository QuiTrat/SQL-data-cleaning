# SQL-data-cleaning
This is my first SQL project 
## upload file club_member_info.csv
## upload club_member lên DBeaver

Mô tả dữ liệu
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|


## Clean data
### Full_name:
- Xoá khoảng trắng đầu và cuối:
```
UPDATE club_member_info_cleaned SET full_name = trim(full_name)
```
- Thống nhất font chữ thành uppercase:
  ```
  UPDATE club_member_info_cleaned SET full_name = UPPER(full_name)
  ```
### Age: Update các tuổi không hợp lý:
```
Select full_name, age from club_member_info_cleaned cmic WHERE age >100 or age<0
```
- Điều chỉnh các dòng có số tuổi >100:

```
UPDATE club_member_info_cleaned set age = FLOOR(age/10) where age>100
```
- Điều chỉnh các dòng có số tuổi = 0 thành số tuổi trung bình của toàn bộ dữ liệu:
  
  ```
  SELECT avg(age) FROM club_member_info_cleaned cmic2 / UPDATE club_member_info_cleaned SET age= 41 WHERE age=0
  ```

### Phone: Xoá các số phone không hợp lý

```
SELECT full_name, email, phone, full_address  FROM club_member_info_cleaned cmic WHERE LENGTH(phone) <12
```
  
|full_name|email|phone|full_address|
|---------|-----|-----|------------|
|ANNALIESE ETOILE|aetoile2w@artisteer.com|814-2985|43 Nova Circle,Garden Grove,California|
|AJAY DEGENHARDT|adegenhardtec@chronoengine.com|14-900-1376|45479 Mayer Street,Newport Beach,California|
|SMITTY BULMER|sbulmergm@addthis.com||23370 Forest Dale Street,Pittsburgh,Pennsylvania|
|FRANCISCO PISER|fpiserkc@tamu.edu||0 Northport Center,Alexandria,Virginia|
|MARION HAWLER|mhawler1p@pinterest.com||60701 Crest Line Drive,Fresno,California|
|SHIRLINE ESHMADE|seshmade9h@ed.gov||331 Bellgrove Hill,Richmond,Virginia|
|CIRILLO BARTLOMIEJCZYK|cbartlomiejczykdj@networksolutions.com||4426 Rigney Alley,Henderson,Nevada|
|GAIL CUTLER|gcutlerf2@auda.org.au||242 Homewood Junction,Pittsburgh,Pennsylvania|
|BLONDIE RICCARDO|briccardofn@about.com|43-892-2116|19 Mayer Drive,Chattanooga,Tennessee|
|WILFRID DANILOV|wdanilovix@is.gd||5208 Tennyson Road,Dallas,Texas|
|LANNIE CLEMMEY|lclemmeykj@redcross.org|575-8072|572 Golf Junction,Mountain View,California|
|SHARLA MACIOCIA|smaciocian3@adobe.com|559-115310|141 Badeau Plaza,Fresno,California|
|JOELLA SURR|jsurrpo@meetup.com||775 Boyd Avenue,Houston,Texas|
|CLAYBORNE PENELLI|cpenellirf@apple.com||01412 Dunning Place,Washington,District of Columbia|

- Chuyển số phone về '' cho các số phone không hợp lý:
  ```
  UPDATE club_member_info_cleaned SET phone='' WHERE LENGTH (phone)<12
  ```
  
|full_name|email|phone|full_address|
|---------|-----|-----|------------|
|ANNALIESE ETOILE|aetoile2w@artisteer.com||43 Nova Circle,Garden Grove,California|
|AJAY DEGENHARDT|adegenhardtec@chronoengine.com||45479 Mayer Street,Newport Beach,California|
|SMITTY BULMER|sbulmergm@addthis.com||23370 Forest Dale Street,Pittsburgh,Pennsylvania|
|FRANCISCO PISER|fpiserkc@tamu.edu||0 Northport Center,Alexandria,Virginia|
|MARION HAWLER|mhawler1p@pinterest.com||60701 Crest Line Drive,Fresno,California|
|SHIRLINE ESHMADE|seshmade9h@ed.gov||331 Bellgrove Hill,Richmond,Virginia|
|CIRILLO BARTLOMIEJCZYK|cbartlomiejczykdj@networksolutions.com||4426 Rigney Alley,Henderson,Nevada|
|GAIL CUTLER|gcutlerf2@auda.org.au||242 Homewood Junction,Pittsburgh,Pennsylvania|
|BLONDIE RICCARDO|briccardofn@about.com||19 Mayer Drive,Chattanooga,Tennessee|
|WILFRID DANILOV|wdanilovix@is.gd||5208 Tennyson Road,Dallas,Texas|
|LANNIE CLEMMEY|lclemmeykj@redcross.org||572 Golf Junction,Mountain View,California|
|SHARLA MACIOCIA|smaciocian3@adobe.com||141 Badeau Plaza,Fresno,California|
|JOELLA SURR|jsurrpo@meetup.com||775 Boyd Avenue,Houston,Texas|
|CLAYBORNE PENELLI|cpenellirf@apple.com||01412 Dunning Place,Washington,District of Columbia|

### membership_date:
- kiểm tra date có hợp lý
```SELECT age, membership_date, (2024-
  CASE 
  	  WHEN LENGTH(membership_date)=10 THEN SUBSTRING(membership_date,7)
	  WHEN LENGTH(membership_date)=8 THEN SUBSTRING(membership_date,5)
	  WHEN LENGTH(membership_date)=9 THEN SUBSTRING(membership_date,6)
  END) AS YEAR

  FROM club_member_info_cleaned cmic WHERE (2024-
  CASE 
	  WHEN LENGTH(membership_date)=10 THEN SUBSTRING(membership_date,7)
	  WHEN LENGTH(membership_date)=8 THEN SUBSTRING(membership_date,5)
	  WHEN LENGTH(membership_date)=9 THEN SUBSTRING(membership_date,6)
  END) >age
```
|age|membership_date|YEAR|
|---|---------------|----|
|46|3/12/1921|103|
|52|10/1/1912|112|
|51|2/20/1916|108|
|38|5/8/1912|112|
|36|10/4/1919|105|
|33|3/10/1913|111|
|41|1/8/1912|112|
|37|9/2/1914|110|
|46|5/11/1916|108|
|27|1/31/1915|109|
|52|5/15/1915|109|
|51|3/3/1917|107|
|19|4/30/1915|109|
|67|5/22/1921|103|
|61|10/27/1915|109|
|38|7/5/1915|109|

- Điều chỉnh năm từ 19xx thành 20xx:

```UPDATE club_member_info_cleaned 
SET membership_date = CASE
   WHEN LENGTH(membership_date)=10 AND SUBSTRING(membership_date,7,2)='19' THEN replace(membership_date,SUBSTRING(membership_date,7,2)='19','20')
   WHEN LENGTH(membership_date)=9 AND SUBSTRING(membership_date,6,2)='19' THEN replace(membership_date,SUBSTRING(membership_date,6,2)='19','20')
   WHEN LENGTH(membership_date)=8 AND SUBSTRING(membership_date,5,2)='19' THEN replace(membership_date,SUBSTRING(membership_date,5,2)='19','20')
 END

WHERE
LENGTH(membership_date)=10 AND SUBSTRING(membership_date,7,2)='19'
OR 
LENGTH(membership_date)=9 AND SUBSTRING(membership_date,6,2)='19'
OR 
LENGTH(membership_date)=8 AND SUBSTRING(membership_date,5,2)='19'
```
## Xoá dữ liệu bị trùng

1. Các tên membber bị trùng
```
SELECT full_name, count(full_name)FROM club_member_info_cleaned cmic GROUP BY full_name HAVING count(full_name)>1
```

|full_name|count(full_name)|
|---------|----------------|
|ERWIN HUXTER|3|
|GARRICK REGLAR|2|
|GEORGES PREWETT|2|
|HASKELL BRADEN|2|
|MADDIE MORRALLEE|2|
|NICKI FILLISKIRK|2|
|OBED MACCAUGHEN|2|
|SEYMOUR LAMBLE|2|
|TAMQRAH DUNKERSLEY|2|

   
2. Lọc dữ liệu bị trùng
4. xoá dữ liệu bị trùng

