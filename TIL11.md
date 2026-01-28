امروز ۲۲ ژانویه معادل ۲ بهمن ۱۴۰۴ هست
یه چیز باحال بهش برخوردیم دیروز
ببین ما یه روت داریم به نام ajax-check-discount-code
که میاد کد تخفیف وارد شده رو بررسی میکنه و اگه مشکلی نداشته باشه آیدی اون رو در جدول ذخیره میکنه (جدول سفارش)
اما هنوز نهایی نشده تخفیف
وقتی کاربر سفارش رو نهایی کنه یعنی روت cart_confirm رو فراخوانی کنه
این تخفیف محاسبه میشه و به عنوان snapshot تو جدول order_currency_totals ذخیره میکنه
ما دیدیم یه شخصی تو سفارش کد تخفیف ثبت کرده و مشکلی نداشته و از هر نظر ولید بوده ولی تخفیف محاسبه نشده مقدارش و صفر نوشته شده
خیلی عجیب بود برام
رفتم لاگ کاربر رو با این دستور چک کردم
grep "37.32.18.9" logs/shop.log | grep "Jan 20 08:"
این کاربر (آقای خاکی) آیپی اش رو پیدا کردیم و این بود.
و بررسی کردم 
[pid: 174|app: 0|req: 25/940] 37.32.18.9 () {82 vars in 1826 bytes} [Tue Jan 20 08:11:22 2026] GET / => generated 119535 bytes in 611 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 174|app: 0|req: 26/941] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:27 2026] POST /ajax_search => generated 3 bytes in 3 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 26/942] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:27 2026] POST /ajax_search => generated 3711 bytes in 1774 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 26/943] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:28 2026] POST /ajax_search => generated 3570 bytes in 1714 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 174|app: 0|req: 28/944] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:29 2026] POST /ajax_search => generated 3570 bytes in 3619 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 28/945] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:30 2026] POST /ajax_search => generated 3910 bytes in 4134 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 174|app: 0|req: 29/946] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:30 2026] POST /ajax_search => generated 3883 bytes in 5001 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 28/947] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:31 2026] POST /ajax_search => generated 3891 bytes in 4027 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 174|app: 0|req: 29/948] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:33 2026] POST /ajax_search => generated 3702 bytes in 2578 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 1/949] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:11:34 2026] POST /ajax_search => generated 932 bytes in 1288 msecs (HTTP/1.1 200) 4 headers in 503 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 30/952] 37.32.18.9 () {86 vars in 1925 bytes} [Tue Jan 20 08:11:43 2026] GET /product/109385 => generated 224622 bytes in 531 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 4/954] 37.32.18.9 () {90 vars in 1949 bytes} [Tue Jan 20 08:12:32 2026] POST /order => generated 31 bytes in 31 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 31/955] 37.32.18.9 () {84 vars in 1849 bytes} [Tue Jan 20 08:12:32 2026] GET /cart/summary?_=1768896702947 => generated 786 bytes in 15 msecs (HTTP/1.1 200) 4 headers in 503 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 32/956] 37.32.18.9 () {86 vars in 1919 bytes} [Tue Jan 20 08:12:45 2026] GET /cart => generated 275 bytes in 5 msecs (HTTP/1.1 308) 4 headers in 559 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 5/957] 37.32.18.9 () {86 vars in 1921 bytes} [Tue Jan 20 08:12:45 2026] GET /cart/ => generated 114643 bytes in 139 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 6/958] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:12:47 2026] POST /ajax_update_currency_unit => generated 15148 bytes in 99 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 33/959] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:09 2026] POST /ajax_search => generated 3 bytes in 3 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 8/960] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:09 2026] POST /ajax_search => generated 3711 bytes in 1399 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 34/961] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:09 2026] POST /ajax_search => generated 4087 bytes in 2129 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 8/962] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:11 2026] POST /ajax_search => generated 3570 bytes in 1303 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 36/963] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:13 2026] POST /ajax_search => generated 3570 bytes in 1281 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 9/964] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:13 2026] POST /ajax_search => generated 3883 bytes in 1216 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 37/965] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:14 2026] POST /ajax_search => generated 3910 bytes in 1322 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 11/966] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:15 2026] POST /ajax_search => generated 3891 bytes in 1671 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 37/967] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:15 2026] POST /ajax_search => generated 3388 bytes in 1346 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 11/968] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:16 2026] POST /ajax_search => generated 1216 bytes in 1808 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 38/969] 37.32.18.9 () {86 vars in 1930 bytes} [Tue Jan 20 08:13:21 2026] GET /product/119217 => generated 219401 bytes in 515 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 12/970] 37.32.18.9 () {90 vars in 1949 bytes} [Tue Jan 20 08:13:27 2026] POST /order => generated 31 bytes in 33 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 39/971] 37.32.18.9 () {84 vars in 1849 bytes} [Tue Jan 20 08:13:27 2026] GET /cart/summary?_=1768896801503 => generated 1340 bytes in 19 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 13/972] 37.32.18.9 () {86 vars in 1921 bytes} [Tue Jan 20 08:13:31 2026] GET /cart/ => generated 117651 bytes in 95 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 14/973] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:13:31 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 85 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 40/974] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:13:31 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 119 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 41/975] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:37 2026] POST /ajax_search => generated 3 bytes in 3 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 0)
[pid: 186|app: 0|req: 43/976] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:38 2026] POST /ajax_search => generated 3576 bytes in 1277 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 44/977] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:39 2026] POST /ajax_search => generated 3579 bytes in 2734 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 16/978] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:38 2026] POST /ajax_search => generated 3711 bytes in 5510 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 17/979] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:37 2026] POST /ajax_search => generated 4087 bytes in 6543 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 17/980] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:43 2026] POST /ajax_search => generated 1135 bytes in 1721 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 45/981] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:40 2026] POST /ajax_search => generated 3579 bytes in 4750 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 186|app: 0|req: 45/982] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:42 2026] POST /ajax_search => generated 3611 bytes in 3196 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 2/983] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:43 2026] POST /ajax_search => generated 1698 bytes in 5354 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 2/984] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:13:43 2026] POST /ajax_search => generated 1135 bytes in 5398 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 18/985] 37.32.18.9 () {86 vars in 1930 bytes} [Tue Jan 20 08:13:59 2026] GET /product/154135 => generated 224976 bytes in 665 msecs (HTTP/1.1 200) 4 headers in 514 bytes (2 switches on core 0)
[pid: 198|app: 0|req: 19/986] 37.32.18.9 () {90 vars in 1949 bytes} [Tue Jan 20 08:14:07 2026] POST /order => generated 31 bytes in 21 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 1)
[pid: 210|app: 0|req: 3/987] 37.32.18.9 () {84 vars in 1849 bytes} [Tue Jan 20 08:14:07 2026] GET /cart/summary?_=1768896838857 => generated 1882 bytes in 14 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 4/988] 37.32.18.9 () {86 vars in 1911 bytes} [Tue Jan 20 08:14:16 2026] GET / => generated 119535 bytes in 753 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 21/990] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:23 2026] POST /ajax_search => generated 3 bytes in 4 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 23/991] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:25 2026] POST /ajax_search => generated 3570 bytes in 1257 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 24/992] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:26 2026] POST /ajax_search => generated 3570 bytes in 2844 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 210|app: 0|req: 6/993] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:24 2026] POST /ajax_search => generated 4087 bytes in 5869 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 6/994] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:24 2026] POST /ajax_search => generated 3711 bytes in 5706 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 198|app: 0|req: 25/995] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:26 2026] POST /ajax_search => generated 3883 bytes in 4887 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 222|app: 0|req: 2/996] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:29 2026] POST /ajax_search => generated 3883 bytes in 2133 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 198|app: 0|req: 25/997] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:28 2026] POST /ajax_search => generated 3910 bytes in 3433 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 2/998] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:30 2026] POST /ajax_search => generated 3898 bytes in 1941 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 210|app: 0|req: 8/999] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:32 2026] POST /ajax_search => generated 3898 bytes in 2017 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 8/1000] 37.32.18.9 () {90 vars in 1990 bytes} [Tue Jan 20 08:14:32 2026] POST /ajax_search => generated 944 bytes in 1917 msecs (HTTP/1.1 200) 4 headers in 503 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 3/1001] 37.32.18.9 () {86 vars in 1925 bytes} [Tue Jan 20 08:14:37 2026] GET /product/145554 => generated 205263 bytes in 591 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 222|app: 0|req: 4/1002] 37.32.18.9 () {90 vars in 1949 bytes} [Tue Jan 20 08:14:55 2026] POST /order => generated 31 bytes in 24 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 1)
[pid: 210|app: 0|req: 9/1003] 37.32.18.9 () {84 vars in 1849 bytes} [Tue Jan 20 08:14:55 2026] GET /cart/summary?_=1768896877034 => generated 2445 bytes in 15 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 10/1004] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:03 2026] POST /ajax_search => generated 3 bytes in 3 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 1)
[pid: 210|app: 0|req: 11/1005] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:05 2026] POST /ajax_search => generated 3570 bytes in 1142 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 13/1006] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:06 2026] POST /ajax_search => generated 3570 bytes in 3094 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 6/1007] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:04 2026] POST /ajax_search => generated 4087 bytes in 6327 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 222|app: 0|req: 7/1008] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:04 2026] POST /ajax_search => generated 3711 bytes in 6221 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 210|app: 0|req: 14/1009] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:06 2026] POST /ajax_search => generated 3883 bytes in 4372 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 222|app: 0|req: 7/1010] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:10 2026] POST /ajax_search => generated 1276 bytes in 1382 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 210|app: 0|req: 14/1011] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:09 2026] POST /ajax_search => generated 3750 bytes in 2458 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 2/1012] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:09 2026] POST /ajax_search => generated 1276 bytes in 5310 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 2/1013] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:15:09 2026] POST /ajax_search => generated 3750 bytes in 5313 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 3/1016] 37.32.18.9 () {86 vars in 1948 bytes} [Tue Jan 20 08:15:22 2026] GET /search?w=1316303071 => generated 74173 bytes in 1271 msecs (HTTP/1.1 200) 4 headers in 513 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 12/1022] 37.32.18.9 () {86 vars in 1944 bytes} [Tue Jan 20 08:15:58 2026] GET /product/146780 => generated 206106 bytes in 427 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 13/1023] 37.32.18.9 () {90 vars in 1949 bytes} [Tue Jan 20 08:16:07 2026] POST /order => generated 31 bytes in 23 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 7/1024] 37.32.18.9 () {84 vars in 1849 bytes} [Tue Jan 20 08:16:07 2026] GET /cart/summary?_=1768896957555 => generated 3024 bytes in 15 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 8/1025] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:16:24 2026] POST /ajax_search => generated 3 bytes in 3 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 9/1026] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:27 2026] POST /ajax_search => generated 3570 bytes in 1166 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 15/1027] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:16:25 2026] POST /ajax_search => generated 4087 bytes in 6245 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 11/1028] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:28 2026] POST /ajax_search => generated 3570 bytes in 2707 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 222|app: 0|req: 16/1029] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:16:25 2026] POST /ajax_search => generated 3711 bytes in 7135 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 12/1030] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:29 2026] POST /ajax_search => generated 3883 bytes in 5071 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 12/1031] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:31 2026] POST /ajax_search => generated 3891 bytes in 3586 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 1/1032] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:33 2026] POST /ajax_search => generated 932 bytes in 1308 msecs (HTTP/1.1 200) 4 headers in 503 bytes (1 switches on core 0)
[pid: 222|app: 0|req: 17/1033] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:31 2026] POST /ajax_search => generated 3910 bytes in 4634 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 222|app: 0|req: 17/1034] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:16:32 2026] POST /ajax_search => generated 3702 bytes in 3734 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 13/1036] 37.32.18.9 () {86 vars in 1938 bytes} [Tue Jan 20 08:16:41 2026] GET /product/109386 => generated 222154 bytes in 589 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 14/1037] 37.32.18.9 () {90 vars in 1948 bytes} [Tue Jan 20 08:16:52 2026] POST /order => generated 31 bytes in 21 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 3/1038] 37.32.18.9 () {84 vars in 1848 bytes} [Tue Jan 20 08:16:52 2026] GET /cart/summary?_=1768897000854 => generated 3571 bytes in 16 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 4/1039] 37.32.18.9 () {86 vars in 1920 bytes} [Tue Jan 20 08:17:05 2026] GET /cart/ => generated 129694 bytes in 144 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 246|app: 0|req: 6/1040] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:17:06 2026] POST /ajax_update_currency_unit => generated 15150 bytes in 502 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 16/1041] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:17:06 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 510 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 7/1042] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:17:06 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 524 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 17/1043] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:17:06 2026] POST /ajax_update_currency_unit => generated 15148 bytes in 528 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 17/1045] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:17:06 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 129 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 7/1045] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:17:06 2026] POST /ajax_update_currency_unit => generated 15150 bytes in 136 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 8/1046] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:43 2026] POST /ajax_search => generated 3 bytes in 3 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 19/1047] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:44 2026] POST /ajax_search => generated 4087 bytes in 2291 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 19/1048] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:45 2026] POST /ajax_search => generated 3711 bytes in 2192 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 9/1049] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:46 2026] POST /ajax_search => generated 3621 bytes in 1137 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 10/1050] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:17:48 2026] POST /ajax_search => generated 1028 bytes in 1145 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 21/1051] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:17:50 2026] POST /ajax_search => generated 1028 bytes in 2163 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 21/1052] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:51 2026] POST /ajax_search => generated 1028 bytes in 2316 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 12/1053] 37.32.18.9 () {90 vars in 1995 bytes} [Tue Jan 20 08:17:53 2026] POST /ajax_search => generated 1028 bytes in 2262 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 22/1054] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:55 2026] POST /ajax_search => generated 1028 bytes in 1155 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 246|app: 0|req: 12/1055] 37.32.18.9 () {90 vars in 1994 bytes} [Tue Jan 20 08:17:54 2026] POST /ajax_search => generated 1028 bytes in 2156 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 23/1056] 37.32.18.9 () {86 vars in 1929 bytes} [Tue Jan 20 08:17:57 2026] GET /product/189679 => generated 222930 bytes in 544 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 13/1057] 37.32.18.9 () {90 vars in 1948 bytes} [Tue Jan 20 08:18:24 2026] POST /order => generated 31 bytes in 35 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 24/1058] 37.32.18.9 () {84 vars in 1848 bytes} [Tue Jan 20 08:18:24 2026] GET /cart/summary?_=1768897077551 => generated 4174 bytes in 21 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 25/1059] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:18:33 2026] POST /ajax_search => generated 3 bytes in 4 msecs (HTTP/1.1 200) 3 headers in 487 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 15/1061] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:18:33 2026] POST /ajax_search => generated 4087 bytes in 1985 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 17/1062] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:18:36 2026] POST /ajax_search => generated 3 bytes in 1065 msecs (HTTP/1.1 200) 4 headers in 501 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 27/1063] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:18:34 2026] POST /ajax_search => generated 3711 bytes in 3640 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 27/1064] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:34 2026] POST /ajax_search => generated 3504 bytes in 3592 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 17/1065] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:37 2026] POST /ajax_search => generated 3504 bytes in 1198 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 246|app: 0|req: 18/1066] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:38 2026] POST /ajax_search => generated 3436 bytes in 1097 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 29/1067] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:39 2026] POST /ajax_search => generated 3401 bytes in 2345 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 29/1068] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:40 2026] POST /ajax_search => generated 3651 bytes in 2272 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 258|app: 0|req: 2/1069] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:42 2026] POST /ajax_search => generated 3651 bytes in 2125 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 30/1070] 37.32.18.9 () {90 vars in 2003 bytes} [Tue Jan 20 08:18:43 2026] POST /ajax_search => generated 1007 bytes in 1181 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 258|app: 0|req: 2/1071] 37.32.18.9 () {90 vars in 2004 bytes} [Tue Jan 20 08:18:43 2026] POST /ajax_search => generated 1007 bytes in 2044 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 31/1072] 37.32.18.9 () {86 vars in 1939 bytes} [Tue Jan 20 08:18:48 2026] GET /product/189678 => generated 225273 bytes in 434 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 258|app: 0|req: 3/1073] 37.32.18.9 () {90 vars in 1949 bytes} [Tue Jan 20 08:18:58 2026] POST /order => generated 31 bytes in 23 msecs (HTTP/1.1 200) 4 headers in 502 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 32/1074] 37.32.18.9 () {84 vars in 1849 bytes} [Tue Jan 20 08:18:58 2026] GET /cart/summary?_=1768897127727 => generated 4745 bytes in 15 msecs (HTTP/1.1 200) 4 headers in 504 bytes (1 switches on core 1)
[pid: 258|app: 0|req: 4/1075] 37.32.18.9 () {86 vars in 1921 bytes} [Tue Jan 20 08:19:10 2026] GET /cart/ => generated 135733 bytes in 191 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 34/1076] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 113 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 35/1077] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 141 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 258|app: 0|req: 6/1078] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 169 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 258|app: 0|req: 7/1079] 37.32.18.9 () {90 vars in 1980 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15150 bytes in 165 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 36/1080] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 157 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 234|app: 0|req: 36/1081] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15148 bytes in 123 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 258|app: 0|req: 8/1082] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15150 bytes in 147 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 0)
[pid: 258|app: 0|req: 8/1083] 37.32.18.9 () {90 vars in 1979 bytes} [Tue Jan 20 08:19:11 2026] POST /ajax_update_currency_unit => generated 15149 bytes in 126 msecs (HTTP/1.1 200) 4 headers in 505 bytes (1 switches on core 1)
[pid: 258|app: 0|req: 10/1087] 37.32.18.9 () {94 vars in 2117 bytes} [Tue Jan 20 08:21:25 2026] POST /cart_confirm => generated 293 bytes in 117 msecs (HTTP/1.1 302) 5 headers in 593 bytes (1 switches on core 1)
[pid: 234|app: 0|req: 39/1088] 37.32.18.9 () {88 vars in 2008 bytes} [Tue Jan 20 08:21:25 2026] GET /?more=353796&error=successful_purchase => generated 119861 bytes in 580 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 0)
[pid: 258|app: 0|req: 11/1090] 37.32.18.9 () {90 vars in 1978 bytes} [Tue Jan 20 08:23:11 2026] POST /ajax-check-discount-code => generated 483 bytes in 27 msecs (HTTP/1.1 200) 4 headers in 503 bytes (1 switches on core 0)
[pid: 270|app: 0|req: 4/1107] 37.32.18.9 () {84 vars in 1896 bytes} [Tue Jan 20 08:28:35 2026] GET /cart/ => generated 108872 bytes in 122 msecs (HTTP/1.1 200) 4 headers in 514 bytes (1 switches on core 1)

این لاگ هاشه
دقت کنی و تک تک خوندیم لاگ ها رو متوجه شدم که کاربر اول نهایی کرده خرید رو بعد از ۲ دقیقه کد تخفیفش ثبت شده و این واقعا برام عجیب بود چون که وقتی سبد خرید نهایی میشه یعنی سبد خرید خالیه و دیگه باکسی برای وارد کردن کد تخفیف وجود نداره پس چجوری شده که ۲ دقیقه بعد این اتفاق افتاده؟
با مهندس نشستیم پاش و بعد از کلی بررسی به این نتیجه رسیدیم
طرف اومده ایجکس ثبت تخفیف رو کال کرده (یعنی کد تخفیف رو وارد و دکمه ثبت رو زده)
از اونجایی که مشکل اینترنت و ضعیفی اینترنت هست (الان تو همون روزایی هستیم که اغتشاشات داخلی ۱۴۰۴ رخ داده و اینترنت به چوخ رفته)
تو مدت تایم اوتی که ست کرده بودیم جواب نیومده بوده (۵ ثانیه) و تایم اوت داده که خطا از سمت سرور رخ داده و کاربر چک نکرده که پیام اصلا چی بوده
و بعد اومده نهایی کرده سبد خرید رو.
حالا از اونجایی که برای تخفیف تایم اوت خورده ولی خود ریکوئست داره سمت بک اند اجرا میشه و در نهایت جوابی هم نمیگیره سمت فرانت ولی با این حال داره اجرا میشه
بعد از ۲ دقیقه اجرا شده و کد تخفیف براش ثبت شده 
و ما فهمیدیم که ای بابا کاربرای ما چه عجیبن حتی پیام خطا رو هم چک نمیکنن و فکر میکنن ثبت شده
کلی بررسی کردیم و الان نت هم نیست اومدیم تحلیل کنیم چیکار کنیم این اتفاق نیوفته
به چند تا راه حل رسیدیم:
۱- سمت فرانت تایم اوت رو بیشتر کنیم
۲- سمت بک اند موقعی که ایجکس میخواد کد رو ثبت کنه یه شرط دیگه هم بذاریم که این سفارش تایید نهایی نشده باشه
۳- راه حل قطعی تر وبهتر اینه که از کوکی ها استفاده کنیم. چجوری؟ اینطوری که در پایین میگم
ببین همیشه طرز فکر من این بود که فرانت به بک اند یه چیزی رو میفرسته و یه ریسپانس هم میگیره که ببینه موفقیت آمیز هست یا نه
ولی به این فکر نکردم که فرضا یه ریسپانس بگیره و از این ریسپانس تو جاهای دیگه استفاده کنه و ببینه موفقیت اون بخش به جاهای دیگه چجوری میتونه ربط پیدا کنه
ساده شو بخوام بگم اینطوری باید پیاده سازی کنم که وقتی ایجکس فراخوانی شده یه آیدی یونیک برای اون کاربر و تخفیف به فرانت برمیگرده و تو کوکی ذخیره میشه
کوکی هم که یه ساختار کلید ولیو هست و حجم ۴ کیلوبایت داره که تو هارد کاربر ذخیره میشه
این آیدی رو موقع نهایی کردن سبد خرید میفرستیم
اگه توش پر بود که یعنی کاربر تخفیف ثبت کرده و میره تخفیف رو محاسبه میکنه
اگه اون آیدی خالی بود پس یا کاربر وارد نکنه کد تخفیف رو یا اگرم وارد کرده به یه خطایی خورده مثلا تایم اوت پس اون تخفیفی که اگه ثبت شده رو هم منقضی میکنیم
و این خیلی جاذابه
ارتباط دو طرفه بین کلاینت و سرور
یه چیزی مثل asymetric encryption 