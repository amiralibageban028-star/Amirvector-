# Amirvector-
from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import Application, CommandHandler, ContextTypes

BOT_TOKEN = "7915503679"

GROUP = "@Amirvector2025"      # گروه
CHANNEL = "@Amirvictor17"     # کانال پک
PACK_LINK = "https://t.me/Amirvictor17"

async def is_member(bot, chat, user_id):
    try:
        member = await bot.get_chat_member(chat, user_id)
        return member.status in ["member", "administrator", "creator"]
    except:
        return False

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = update.effective_user.id

    in_group = await is_member(context.bot, GROUP, user_id)
    in_channel = await is_member(context.bot, CHANNEL, user_id)

    if in_group and in_channel:
        await update.message.reply_text(
            "✅ عضویت تأیید شد — این هم پک:",
            reply_markup=InlineKeyboardMarkup([
                [InlineKeyboardButton("📦 دریافت پک", url=PACK_LINK)]
            ])
        )
    else:
        buttons = []
        if not in_group:
            buttons.append([InlineKeyboardButton("👥 ورود به گروه", url="https://t.me/Amirvector2025")])
        if not in_channel:
            buttons.append([InlineKeyboardButton("📢 ورود به کانال", url="https://t.me/Amirvictor17")])

        await update.message.reply_text(
            "❌ برای دریافت پک باید عضو هر دو شوید:",
            reply_markup=InlineKeyboardMarkup(buttons)
        )

app = Application.builder().token(BOT_TOKEN).build()
app.add_handler(CommandHandler("start", start))
app.run_polling()
