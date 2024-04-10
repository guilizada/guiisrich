import os
import time
import random
import telebot
from datetime import datetime
from telebot.types import InlineKeyboardButton, InlineKeyboardMarkup
import bd

api_key = '6925897926:AAGj6QOyQCOGi9Qa3Gxa15nQuSVp3bFVXzM'  # Substitua pelo seu próprio token
chat_id = '-1002086698242'  # Substitua pelo ID do seu canal

bot = telebot.TeleBot(token=api_key)

# Defina as funções ALERT_GALE1 e DELETE_GALE1 como antes
def ALERT_GALE1():
    h = datetime.now().hour
    m = datetime.now().minute + 1
    s = datetime.now().second
    if h <= 9:
        h = f'0{h}'
    if m <= 9:
        m = f'0{m}'
    if s <= 9:
        s = f'0{s}'
    message_id = bot.send_message(chat_id=chat_id, text=f'''
🔍 Possivel Entrada Detectada''').message_id
    bd.message_ids1 = message_id
    time.sleep(15)
    bd.message_delete1 = True

def DELETE_GALE1():
    if bd.message_delete1 == True:
        bot.delete_message(chat_id=chat_id, message_id=bd.message_ids1)
        bd.message_delete1 = False

# Lista todos os arquivos jpg no diretório especificado
def listar_arquivos_jpg(diretorio):
    arquivos_jpg = [f for f in os.listdir(diretorio) if f.endswith('.jpg')]
    return arquivos_jpg

# Resto do código
def button_link():
    markup = InlineKeyboardMarkup()
    markup.row_width = 2
    markup.add(InlineKeyboardButton(text="Aposte Aqui💸", url="https://www.youtube.com"))
    return markup

while True:
    h = datetime.now().hour
    m = datetime.now().minute + 2
    s = datetime.now().second
    if h <= 9:
        h = f'0{h}'
    if m <= 9:
        m = f'0{m}'
    if s <= 9:
        s = f'0{s}'
    print(f'{h}:{m}:{s}')

    minas_configuracoes = [3, 4]

    # Escolhe aleatoriamente a quantidade de minas
    minas = random.choice(minas_configuracoes)
    
    ALERT_GALE1()  # Chama a função de alerta

    DELETE_GALE1()  # Chama a função de exclusão do alerta

    # Lista os arquivos jpg no diretório onde o script está sendo executado
    diretorio = os.path.dirname(os.path.abspath(__file__))
    arquivos_jpg = listar_arquivos_jpg(diretorio)
    
    # Escolhe aleatoriamente um arquivo jpg
    jpg_escolhido = random.choice(arquivos_jpg)

    # Monta a mensagem com o arquivo jpg
    message_text = f'''
 ✅SINAL CONFIRMADO ✅ 

💎guiisrich_

🕛 Válido até: {h}:{m}                                                   
💣 Minas: {minas}
📊 Chance de acerto: 100.00%
🔁 Nº de entradas: 3

'''

    # Envia a mensagem com o arquivo jpg
    with open(os.path.join(diretorio, jpg_escolhido), 'rb') as photo:
        bot.send_photo(chat_id=chat_id, photo=photo, caption=message_text, reply_markup=button_link())

    time.sleep(120)

    # Envia mensagem de sinal finalizado
    bot.send_message(chat_id=chat_id, text=f'''
🔴Sinal finalizado:{h}:{m}🔴
  

    ''')

    time.sleep(15)
    
