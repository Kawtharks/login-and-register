#أولا أنشأنا المشروع والتطبيق
حملنا مكاتب 
djangorestframework ,jangorestframework-simplejwt 
إضافة rest-framework , app2 اسم التطبيق
to installed_aps 
ثم اضافة
AUTH_USER_MODEL = 'app2.CustomUser' لأعلام django أنني أريد نسخة خاصة من النموذج قابلة للتعديل مستقبلاً
in settings.py
أنشأنا serlizer.py
مهمته الحصول على modelثم يحدد الحقول المطلوبة ثم باستخدام التابع validate_password يشفر كلمة السر قبل حفظها
في الviews
استدعاء لمكاتب generic,permissions
الهدف منها استخدام generic.createapiview لانشاء مستخدمين جدد
وربط مع  serializer ,
يستطيع الوصول لصفحة  permission_classes = [permissions.AllowAny] باستخدام
register أي أحد دون مصادقة
بالنسبة لlogin استخدمنا TokenObtainPairView تأخذ username ,password وتتحقق من البيانات ثم تعطي jwt refresh and access token
ثم وضعنا دالة profile_view لا تستجيب إلا لطلبات get ولا يستطيع الوصول لها إلا من لديه  JWT access token 
الاستجابة تكون عبارة عن id المستخدم واسمه وايميله 
ثم كالعادة نربط views مع url
والربط بين الurl الداخلي للتطبيق والخارجي للمشروع
يجب القيام بpython manage.py makemigrations لأننا نتعامل مع model datbase  sqlite
التنفيذ في postman بإدخال url لكل صفحة أولاً regiter ثم login الذي يعطي token 
register لا يقبل ادخال نفس المستخدم مرتين يرسل رسالة الاسم موجود مسبقاً