این کد رو ببین
    dai_cookie          = str(request.cookies.get('dai', None)) # dai stands for discount attempt id
    order_discount_id   = active_cart.get('discount_id', None)
    discount_attempt_id = str(active_cart.get('discount_attempt_id', None))
    apply_discount      = False

    if dai_cookie == discount_attempt_id:
        apply_discount = True
    for currency, amount in totals_by_currency.items():
        if amount > 0:  # Only insert if there is an amount for that currency

            if not apply_discount:
                discount_id             = None
                discount_code           = None
                discount_type           = None
                discount_value          = None
                discount_amount         = None
                discount_max_amount     = None
                discount_min_purchase   = None
            else:
                discount_id                                 = order_discount_id
                discount_setting                            = get_discount_setting_per_currency(discount_id, currency)
                discount                                    = get_discount(discount_id)
                discount_type                               = discount.get('discount_type', None)
                discount_code                               = discount.get('code', None)
                discount_value                              = discount_setting.get('value', None)
                discount_max_amount                         = discount_setting.get('max_amount', None)
                discount_min_purchase                       = discount_setting.get('min_purchase', None)
                _, valid_currencies, invalid_currencies, _  = check_min_purchase_validity(active_cart_id)
                discount_amount, _                          = calculate_discount_amount_per_currency(discount_id, discount_type, amount, currency, valid_currencies, invalid_currencies)

            cursor.execute("""
                INSERT INTO order_currency_totals (order_id, currency_unit, total_amount, discount_id, discount_code, discount_type, discount_value, discount_amount, discount_max_amount, discount_min_purchase)
                VALUES (%s, %s, %s, %s, %s, %s, %s, %s, %s, %s)
            """, (active_cart_id, currency, amount, discount_id, discount_code, discount_type, discount_value, discount_amount, discount_max_amount, discount_min_purchase))

این کد یه جایی خطا میزنه
ببین در یه صورت ممکنه apply_discount برابر True بشه
بعد میره تو قسمت else حلقه و تابع calculate_discount_amount_per_currency
رو ران میکنه و خطا میده چون اصلا دیسکونت آیدی نداریم
اگه هم dia_cookie برابر None باشه هم discount_attempt_id
وقتی تبدیل به string میشه
خطا میده
چون هردو میشه استرینگ None
و در این صورت هر دو برابر هستن و سیستم خراب میشه
اول اینکه من گفتم 

    dai_cookie          = request.cookies.get('dai', None) # dai stands for discount attempt id
    order_discount_id   = active_cart.get('discount_id', None)
    discount_attempt_id = active_cart.get('discount_attempt_id', None)
    apply_discount      = False

    if (discount_attempt_id or dai_cookie) and (dai_cookie == discount_attempt_id):
        apply_discount = True

و در ثانی خود تابع calculate_discount_amount_per_currency رو اولش همچین شرطی گذاشتم
def calculate_discount_amount_per_currency(discount_id, discount_type, total_price_before_discount, currency_unit, valid_currencies, invalid_currencies):
    if not discount_id:
        discount_amount = 0
        final_price = total_price_before_discount
        return discount_amount, total_price_before_discount

اینطوری دیگه هیچ راه در رویی نذاشتم
یعنی خود تابع به تنهایی درست کار میکنه حتی اگه برنامه نویس یادش بره که جایی که این تابع رو استفاده میکنه درست و درمون ولیدیت بکنه
پس باید یادم باشه در کنار رعایت اصل Single Responsibility
خود تابع هم ولیدیت بکنه چیزای اولیه و اصولی رو 
و فکر کنم این ناقض سینگل ریسپانسیبیلیتی نیست
و باید همه جا ورودی های غیر معتبر هندل بشن چون این وظیفه ذاتی خود تابع و کلاس و ... هست

طبق اصول Clean Code و SOLID:
هر تابع باید مطمئن باشد که با ورودی نامعتبر Crash نمی‌کند.