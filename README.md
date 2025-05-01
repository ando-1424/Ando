# Ando
Programming 
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>توظيف المبرمجين - EliteDevs</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #3b82f6;
            --primary-dark: #2563eb;
            --secondary: #10b981;
            --dark: #1e293b;
            --light: #f8fafc;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Tajawal', sans-serif;
        }
        
        body {
            background-color: #f1f5f9;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        /* زر التقديم الرئيسي */
        .apply-btn {
            position: relative;
            background: linear-gradient(135deg, var(--primary), var(--secondary));
            color: white;
            border: none;
            padding: 16px 32px;
            font-size: 18px;
            font-weight: bold;
            border-radius: 50px;
            cursor: pointer;
            overflow: hidden;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
            z-index: 1;
        }
        
        .apply-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
        }
        
        .apply-btn:active {
            transform: translateY(1px);
        }
        
        .apply-btn::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: linear-gradient(135deg, var(--secondary), var(--primary));
            opacity: 0;
            z-index: -1;
            transition: opacity 0.3s ease;
        }
        
        .apply-btn:hover::before {
            opacity: 1;
        }
        
        /* نافذة التقديم */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 100;
            justify-content: center;
            align-items: center;
            animation: fadeIn 0.3s;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        
        .modal-content {
            background-color: white;
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 500px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            transform: scale(0.9);
            animation: scaleUp 0.3s forwards;
            position: relative;
        }
        
        @keyframes scaleUp {
            to { transform: scale(1); }
        }
        
        .close-btn {
            position: absolute;
            top: 15px;
            left: 15px;
            font-size: 24px;
            cursor: pointer;
            color: var(--dark);
            transition: color 0.3s;
        }
        
        .close-btn:hover {
            color: var(--primary);
        }
        
        .form-title {
            text-align: center;
            margin-bottom: 20px;
            color: var(--dark);
            font-size: 24px;
        }
        
        .input-group {
            margin-bottom: 20px;
        }
        
        .input-group label {
            display: block;
            margin-bottom: 8px;
            color: var(--dark);
            font-weight: bold;
        }
        
        .input-group input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        .input-group input:focus {
            outline: none;
            border-color: var(--primary);
        }
        
        .submit-btn {
            width: 100%;
            padding: 14px;
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        
        .submit-btn:hover {
            background-color: var(--primary-dark);
        }
        
        /* أزرار التواصل الإضافية */
        .social-btns {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-top: 30px;
        }
        
        .social-btn {
            width: 50px;
            height: 50px;
            border-radius: 50%;
            display: flex;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 20px;
            cursor: pointer;
            transition: transform 0.3s, box-shadow 0.3s;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .social-btn:hover {
            transform: translateY(-5px) scale(1.1);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .discord { background-color: #5865F2; }
        .telegram { background-color: #26A5E4; }
        .github { background-color: #333; }
        .email { background-color: #EA4335; }
        
        /* رسالة النجاح */
        .success-message {
            display: none;
            text-align: center;
            padding: 20px;
        }
        
        .success-message i {
            font-size: 50px;
            color: var(--secondary);
            margin-bottom: 15px;
        }
        
        .success-message h3 {
            color: var(--dark);
            margin-bottom: 10px;
        }
        
        .success-message p {
            color: #64748b;
        }
    </style>
</head>
<body>
    <!-- زر التقديم الرئيسي -->
    <button class="apply-btn" id="applyBtn">
        <i class="fas fa-code"></i> قدم كمبرمج
    </button>
    
    <!-- نافذة التقديم -->
    <div class="modal" id="applyModal">
        <div class="modal-content">
            <span class="close-btn" id="closeBtn">&times;</span>
            
            <div id="formContainer">
                <h2 class="form-title">تقديم طلب مبرمج</h2>
                <form id="applicationForm">
                    <div class="input-group">
                        <label for="name">الاسم الكامل</label>
                        <input type="text" id="name" required>
                    </div>
                    
                    <div class="input-group">
                        <label for="email">البريد الإلكتروني</label>
                        <input type="email" id="email" required>
                    </div>
                    
                    <div class="input-group">
                        <label for="specialty">التخصص</label>
                        <input type="text" id="specialty" placeholder="مثال: تطوير مواقع، بوتات ديسكورد..." required>
                    </div>
                    
                    <button type="submit" class="submit-btn">إرسال الطلب</button>
                </form>
                
                <!-- أزرار التواصل الإضافية -->
                <div class="social-btns">
                    <div class="social-btn discord" title="انضم لسيرفر الديسكورد">
                        <i class="fab fa-discord"></i>
                    </div>
                    <div class="social-btn telegram" title="انضم لقناة التليجرام">
                        <i class="fab fa-telegram"></i>
                    </div>
                    <div class="social-btn github" title="زورنا على جيت هاب">
                        <i class="fab fa-github"></i>
                    </div>
                    <div class="social-btn email" title="راسلنا عبر الإيميل">
                        <i class="fas fa-envelope"></i>
                    </div>
                </div>
            </div>
            
            <!-- رسالة النجاح -->
            <div class="success-message" id="successMessage">
                <i class="fas fa-check-circle"></i>
                <h3>تم إرسال طلبك بنجاح!</h3>
                <p>سنقوم بالتواصل معك عبر البريد الإلكتروني خلال 24 ساعة</p>
            </div>
        </div>
    </div>
    
    <script>
        // عناصر DOM
        const applyBtn = document.getElementById('applyBtn');
        const applyModal = document.getElementById('applyModal');
        const closeBtn = document.getElementById('closeBtn');
        const applicationForm = document.getElementById('applicationForm');
        const formContainer = document.getElementById('formContainer');
        const successMessage = document.getElementById('successMessage');
        
        // فتح النافذة
        applyBtn.addEventListener('click', () => {
            applyModal.style.display = 'flex';
            document.body.style.overflow = 'hidden';
        });
        
        // إغلاق النافذة
        closeBtn.addEventListener('click', closeModal);
        applyModal.addEventListener('click', (e) => {
            if (e.target === applyModal) closeModal();
        });
        
        function closeModal() {
            applyModal.style.display = 'none';
            document.body.style.overflow = 'auto';
        }
        
        // إرسال النموذج
        applicationForm.addEventListener('submit', (e) => {
            e.preventDefault();
            
            // جمع بيانات النموذج
            const formData = {
                name: document.getElementById('name').value,
                email: document.getElementById('email').value,
                specialty: document.getElementById('specialty').value,
                timestamp: new Date().toISOString()
            };
            
            // هنا يمكنك إضافة كود الإرسال إلى الخادم
            console.log('تم إرسال البيانات:', formData);
            
            // عرض رسالة النجاح
            formContainer.style.display = 'none';
            successMessage.style.display = 'block';
            
            // إغلاق النافذة بعد 3 ثواني
            setTimeout(() => {
                closeModal();
                formContainer.style.display = 'block';
                successMessage.style.display = 'none';
                applicationForm.reset();
            }, 3000);
        });
        
        // تأثيرات الأزرار الإجتماعية
        const socialBtns = document.querySelectorAll('.social-btn');
        
        socialBtns.forEach(btn => {
            btn.addEventListener('mouseenter', () => {
                const icon = btn.querySelector('i');
                icon.style.transform = 'scale(1.2)';
            });
            
            btn.addEventListener('mouseleave', () => {
                const icon = btn.querySelector('i');
                icon.style.transform = 'scale(1)';
            });
            
            btn.addEventListener('click', () => {
                // إضافة روابط التواصل هنا
                const type = btn.classList[1];
                let url = '';
                
                switch(type) {
                    case 'discord':
                        url ='https://discord.gg/BP4n8Sz9uC';
                        break;
                    case 'telegram':
                        url = 'https://t.me/yourchannel';
                        break;
                    case 'github':
                        url = 'https://github.com/yourprofile';
                        break;
                    case 'email':
                        url = 'tlion9875@gmail.com';
                        break;
                }
                
                window.open(url, '_blank');
            });
        });
        
        // تأثيرات عند التمرير
        window.addEventListener('scroll', () => {
            const scrollY = window.scrollY;
            applyBtn.style.transform = `translateY(${scrollY * 0.2}px)`;
        });
    </script>
</body>
</html>
