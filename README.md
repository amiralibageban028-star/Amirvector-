# Amirvector-
from telegram import Update, InlineKeyboardButton, InlineKeyboardMarkup
from telegram.ext import Application, CommandHandler, ContextTypes

BOT_TOKEN = "توکن_رباتت"
GROUP_USERNAME = "@Amirvector2025"
PACK_LINK = "https://t.me/Amirvictor17"

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    user_id = update.effective_user.id

    try:
        member = await context.bot.get_chat_member(GROUP_USERNAME, user_id)

        if member.status in ["member", "administrator", "creator"]:
            await update.message.reply_text(
                "✅ عضو گروه هستی!\nاین هم پک تو:",
                reply_markup=InlineKeyboardMarkup([
                    [InlineKeyboardButton("📦 دریافت پک", url=PACK_LINK)]
                ])
            )
        else:
            raise Exception()

    except:
        await update.message.reply_text(
            "❌ برای دریافت پک باید عضو گروه بشی:",
            reply_markup=InlineKeyboardMarkup([
                [InlineKeyboardButton("👥 ورود به گروه", url="https://t.me/Amirvector2025")]
            ])
        )

app = Application.builder().token(BOT_TOKEN).build()
app.add_handler(CommandHandler("start", start))
app.run_polling()
