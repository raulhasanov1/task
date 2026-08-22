# Linux `sed` və Python-da `EOF` (End of File) Dokumentasiyası

Bu layihə Linux əməliyyat sistemində mətn emalı üçün istifadə olunan `sed` komandası və proqramlaşdırmada faylın sonunu təyin edən `EOF` anlayışı, həmçinin Python-dakı `EOFError` xətaları haqqında ətraflı məlumatı ehtiva edir.

---

## 1. `sed` Komandası Nədir?

`sed` (stream editor) – mətn verilənlərinin ardıcıl axınına qabaqcadan müəyyən olunmuş müxtəlif mətn çevirmələri tətbiq edən mətn redaktoru (eləcə də proqramlaşdırma dili). 

* **Tarixçəsi:** İlkin variantı 1973-74-cü illərdə Bell Labs əməkdaşı Li Makmahon (Lee E. McMahon) tərəfindən UNIX-utilit kimi yazılıb. 
* **İş prinsipi:** Hazırda `sed` faktiki olaraq komanda sətri ilə işi dəstəkləyən istənilən əməliyyat sistemində işləyir. Olduqca dolaşıq proqram olsa da, çox güclüdür.
* **Fərqi:** `sed` giriş axınını (adətən, fayl) sətirbəsətir qəbul edir, `sed`-skriptlə müəyyən olunmuş qaydalara uyğun olaraq hər bir sətri redaktə edir və nəticəni çıxış axınına verir. Adi mətn redaktorlarından fərqli olaraq, `sed` öncə komandalar toplusunu özünə yükləyir, sonra ise bütün komandaları mətnin hər bir sətrinə tətbiq edir. Eyni anda yaddaşda yalnız bir sətir ola bildiyindən, `sed` istənilən böyüklükdə mətn fayllarını emal edə bilər.

### İstifadə Nümunəsi:
\`\`\`bash
sed 's/regexp/replacement/g' inputFileName > outputFileName
\`\`\`

---

## 2. `EOF` (End of File - Faylın Sonu) Anlayışı

Faylın sonu – bəzən proqram tərəfindən faylın axırıncı baytında yerləşdirilən kod. `EOF` simvolu əməliyyat sisteminə verilənlərin sonunu bildirən nişandır. 

* **Niyə vacibdir?** Bu gərəksiz görünə bilər, ancaq `EOF` simvolu faylın gerçək sonluğunu göstərdiyindən çox zaman faydalıdır: çünki fayl üçün tam sayda klaster ayrıldığından, faylın həqiqi sonluğu klasterin ortasına düşdükdə, həmin sonluq faylın fiziki sonluğu (faylın axırıncı klasterinin axırıncı baytı) ilə üst-üstə düşməyəcək.
* **Kodlaşdırma:** ASCII kodunda `EOF` simvolu onluq **26** (onaltılıq **1Ah**) qiyməti ilə və ya **Control+Z** idarəedici simvolu ilə göstərilib.

---

## 3. Python-da Fayllarla İşləyərkən EOF

Python-da fayllarla işləyərkən `EOF` (End of File - Faylın Sonu), oxuma əməliyyatının faylın bitdiyi yerə çatdığını bildirən bir anlayışdır. Digər bəzi proqramlaşdırma dillərindən fərqli olaraq, Python-da xüsusi bir `EOF` funksiyası və ya xətası yoxdur. Bunun əvəzinə faylın sonuna çatdığımızı qaytarılan boş dəyərlərdən (`''`) başa düşürük.

---

## 4. "EOFError: EOF when reading a line" Xətası Nədir?

Bu xəta Python-da `input()` funksiyası heç bir məlumat oxumadan "faylın sonu" (EOF) şərtinə rast gəldikdə baş verir. 

**EOFError-un Yaranma Kontekstləri:**
* **İnteraktiv Giriş:** Skriptdə istifadəçi girişi gözləyən `input()` funksiyasından istifadə edildikdə, lakin heç bir məlumat əldə olunmadıqda.
* **Faylın İdarə Edilməsi:** `readline()` və ya `read()` kimi metodlardan istifadə edərək faylın sonundan o tərəfə oxumağa cəhd etdikdə.
* **Avtomatlaşdırılmış Testlər:** Skriptlər və ya testlər istifadəçi girişinin gözlənildiyi kimi təmin edilmədiyi mühitdə işlədildikdə.


