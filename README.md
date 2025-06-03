Để tạo bot Telegram trên Google Cloud chạy bằng SSH, bạn cần thực hiện các bước sau:
1. Chuẩn bị
•  Tài khoản Telegram: Đã cài ứng dụng Telegram và có tài khoản.
•  Google Cloud Platform (GCP): Đăng ký tài khoản GCP, tạo một project và bật SSH.
•  Ngôn ngữ lập trình: Dùng Python (khuyến nghị vì đơn giản và có nhiều thư viện hỗ trợ).
2. Tạo bot Telegram
•  Mở Telegram, tìm @BotFather.
•  Gõ lệnh /start, sau đó /newbot.
•  Đặt tên và username cho bot (username phải kết thúc bằng “bot”, ví dụ: @MyBot).
•  Sau khi tạo, bạn nhận được Token API. Lưu cẩn thận token này.
3. Cài đặt môi trường trên Google Cloud
•  Tạo VM trên GCP:
	•  Vào GCP Console, tạo một máy ảo (Compute Engine > VM Instances).
	•  Chọn hệ điều hành Ubuntu (khuyến nghị Ubuntu 20.04 LTS).
	•  Cấu hình firewall để mở cổng 443 (cho webhook) hoặc các cổng cần thiết.
•  Kết nối SSH:
	•  Trong GCP, vào VM instance, chọn SSH để mở terminal.
	•  Hoặc dùng công cụ như PuTTY hoặc terminal local với gcloud compute ssh [INSTANCE_NAME].
4. Cài đặt môi trường lập trình trên VM
•  Cập nhật hệ thống:
#sudo apt update && sudo apt upgrade -y
Cài Python và pip:
#sudo apt install python3 python3-pip -y
Cài thư viện Python cho bot Telegram:
#pip3 install python-telegram-bot
5. Viết mã bot Telegram
•  Tạo file Python (ví dụ: bot.py):
#nano bot.py
Ví dụ 

#"from telegram.ext import Updater, CommandHandler

def start(update, context):
    update.message.reply_text('Xin chào! Tôi là bot của bạn.')
def main():
    # Thay YOUR_TOKEN bằng token từ BotFather
    updater = Updater("YOUR_TOKEN", use_context=True)
    dp = updater.dispatcher
    dp.add_handler(CommandHandler("start", start))
    updater.start_polling()
    updater.idle()
if __name__ == '__main__':
    main()"

6. Chạy bot
•  Chạy file Python:
#python3 bot.py
•  Bot sẽ hoạt động, thử vào Telegram, nhắn /start để kiểm tra.
7. Chạy bot nền
•  Để bot chạy liên tục, dùng screen hoặc nohup:
screen
#python3 bot.py
Nhấn Ctrl+A, sau đó D để thoát screen mà vẫn chạy bot.
.Hoặc dùng nohup:
 #nohup python3 bot.py &
