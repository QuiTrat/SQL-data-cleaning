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

- Home work: clean data ghi vào readme các bước clean data
## Clean data
### Full_name:
- Xoá khoảng trắng đầu và cuối: UPDATE club_member_info_cleaned SET full_name = trim(full_name)
- Thống nhất font chữ thành uppercase:UPDATE club_member_info_cleaned SET full_name = UPPER(full_name)

  |full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|ADDIE LUSH|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|SYDEL SHARVELL|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|CONSTANTIN DE LA CRUZ|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|GAYLOR REDHOLE|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|WANDA DEL MAR|44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|JOANN KENEALY|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|JOETE CUDIFF|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|


### Age: Update các tuổi không hợp lý:
- select full_name, age from club_member_info_cleaned cmic WHERE age >100 or age<0
  
- |full_name|age|
|---------|---|
|JORI SANZ|399|
|CARLYE GRAEBER|555|
|SHURWOOD STRUTLEY|544|
|CORBIN HILLAN|499|
|SMITTY BULMER|522|
|LEONORE BOOTHJARVIS||
|AUNDREA VILLAR|277|
|CHERY BATISSE||
|ERINA AUBERT|288|
|BALDWIN RIPPEN|588|
|CHERISE KRISTOFFERSSON|599|
|THORNDIKE PORTINGALE|677|
|HASKELL BRADEN|322|
|MONTAGUE LATHAM|644|
|VIRGINA HUBBOCK||
|ALVA DELL 'ORTO|411|
|DENNI STALLARD|633|
|CATHRINE JONSON|222|

- Điều chỉnh các dòng có số tuổi >100: UPDATE club_member_info_cleaned set age = FLOOR(age/10) where age>100
- Điều chỉnh các dòng có số tuổi = 0 thành số tuổi trung bình của toàn bộ dữ liệu: SELECT avg(age) FROM club_member_info_cleaned cmic2 / UPDATE club_member_info_cleaned SET age= 41 WHERE age=0

### Phone: Xoá các số phone không hợp lý
- SELECT full_name, email, phone, full_address  FROM club_member_info_cleaned cmic WHERE LENGTH(phone) <12
  
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

- Chuyển số phone về '' cho các số phone không hợp lý: UPDATE club_member_info_cleaned SET phone='' WHERE LENGTH (phone)<12
  
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
SELECT age, membership_date, (2024-
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
END) >100
  
