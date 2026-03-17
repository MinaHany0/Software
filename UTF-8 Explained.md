<a href = "https://www.youtube.com/watch?v=vpSkBV5vydg">Click here for Video Link</a>

- at first people wanted to represent letters and number ans sybmols but if no standard was there, it would be a mess
- many companies made different standards, so machines couldn't communicate well
- so ASCI was made - 7 Bit encoding
- after a bit other languages needed to be added to the computer![[UTF-8 Explained-20260317172135033.webp]]
- then UNICODE appeared ![[UTF-8 Explained-20260317172207342.webp]]
- so Unicode at the first stage is just all letters numbered but not yet coded into ASCI as the  ASCII has 7 bits so  it can't represent all of the letters
-  ف عندنا حل سهل وهو اننا نغير كل التشفير من استخدان بايت واحدة الى استخدام 2 بايت
- ولكن الحل دا مش backward compatible يعنى كل ال software القديم هيبوظ و ل1لك عملوا حل عبقرى 
  وهو ان هيسخدموا الbit ال8 عشان يوضح كل الencoding معمول فى بايت واحدة ولا اكتر و كدا هيكون backward compatible ![[UTF-8 Explained-20260317174813012.webp]]
-  ولكن ظهر مشكلة تانية و هى ان الdecoder الجديد بيقرا القيم ولكن القديم مش بيقرا الجديد
- ![[UTF-8 Explained-20260317175130467.webp]]![[UTF-8 Explained-20260317175143135.webp]]
- so the new solution is for all the new encoding to have the 8th-bit set to "1" so we lose 1 bit from all bytes like this:![[UTF-8 Explained-20260317175237906.webp]]
- المشكلة الجديدة هى ازاى هنعرف الحروف بدات فى اى بايت اذا كلهم بيبداوا ب 1 ؟؟؟
- اجابة صحيحة : الleading byte هتبدا ب 11  وال continuation byte هتبدا ب 10 , وال ASCII هيبدا ب 0 اصلا  ![[UTF-8 Explained-20260317180132287.webp]]
- and they called this UTF-8  (Unicode Transformation format) where unicode is the big table we all agreed to represent using certain numbers and then this method for representation is the transformation format ![[UTF-8 Explained-20260317180206502.webp]]
- microsoft uses UTF-16 and some others use UTF-32 ![[UTF-8 Explained-20260317180354353.webp]]
- the advantage in the UTF-32 is we can easily find any character in an array of characters , instead of needing to scan the full array to find a certain index (because all of the characters has the same width)
- the this is the final representation ![[UTF-8 Explained-20260317180943972.webp]]
- and so we represent this using hexadecimal code from 00 to FF where is the letter is 
	- 8 to B -> then this is continuation bit
	- C,D -> first byte of a 2 byte unit sequence
	- E -> first byte of a 3 byte unit sequence
	- F -> first byte of a 4 byte unit sequence
- except some are left unused (EF-BF-ED) and if the computer found them, they would be represented with the famous question mark symbol.
- ![[UTF-8 Explained-20260317181535869.webp]]
- ![[UTF-8 Explained-20260317181924070.webp]]
- 