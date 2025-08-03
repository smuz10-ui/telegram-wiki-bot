import telebot
import wikipedia

# Telegram bot token — agar direct dal rahe ho:
TOKEN = '8294596152:AAHwZuFcyFsmgjpT0gsC41Owde49jwc3VlM'
bot = telebot.TeleBot(TOKEN)

# Hindi me Wikipedia set kar diya hai
wikipedia.set_lang("hi")

@bot.message_handler(commands=['start'])
def start_message(message):
    bot.send_message(message.chat.id, "नमस्ते! मुझे कोई भी विषय भेजो, मैं Wikipedia से जानकारी दूँगा।")

@bot.message_handler(func=lambda message: True)
def search_wikipedia(message):
    try:
        summary = wikipedia.summary(message.text, sentences=2)
        bot.send_message(message.chat.id, summary)
    except Exception as e:
        bot.send_message(message.chat.id, "सॉरी, कोई जानकारी नहीं मिली या कुछ गलती हो गई।")

bot.polling()

