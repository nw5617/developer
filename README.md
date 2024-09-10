pip install python-telegram-bot  


from telegram.ext import Updater, CommandHandler

def start(update, context):
    context.bot.send_message(chat_id=update.effective_chat.id, text="Hello, I'm a Movie Bot!")

def request_movie(update, context):
    query = ' '.join(context.args)
    if query:
        # Simulate searching movie links (could be a database or an API)
        movie_links = f"Here are results for {query}:\n[1.4 GB] {query} 1080p\n[740 MB] {query} 720p"
        update.message.reply_text(movie_links)
    else:
        update.message.reply_text("Please specify the movie name.")

def main():
    updater = Updater("YOUR_BOT_TOKEN", use_context=True)
    dp = updater.dispatcher
    
    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(CommandHandler("request", request_movie, pass_args=True))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
