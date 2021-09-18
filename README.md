_C='client.txt'
_B='chatBubble'
_A=True
import requests,json,threading
from urllib.request import urlopen
from zipfile import ZipFile
from time import sleep
from threading import Thread
def upload_bubble(file,comId):
        B=comId;C=file;A=requests.post(f"https://service.narvii.com/api/v1/x{B}/s/chat/chat-bubble/templates/107147e9-05c5-405f-8553-af65d2823457/generate",data=C,headers=cli.headers);D=json.loads(A.text)[_B]['bubbleId'];print(D);A=requests.post(f"https://service.narvii.com/api/v1/x{B}/s/chat/chat-bubble/{D}",data=C,headers=cli.headers)
        try:print(A.status_code)
        except:pass
import amino
try:
        with open(_C,'r')as file_:para=file_.readlines();cli=amino.Client(deviceId=para[2].strip());cli.login(email=para[0].strip(),password=para[1].strip())
except FileNotFoundError:
        with open(_C,'w')as file_:file_.write('email\npassword');print('Please enter your email and password in the file client.txt');print('-----end-----');exit(1)
@cli.event('on_text_message')
def on_text_message(data):
        I=None;C='replyMessage';A=data
        if A.message.type==0:
                if A.message.content.lower()=='!забрать':
                        print('wait')
                        try:
                                B=amino.SubClient(comId=A.comId,profile=cli.profile);B.get_message_info(chatId=A.message.chatId,messageId=A.message.messageId)
                                if A.message.extensions and A.message.extensions.get(C,I)and A.message.extensions[C].get('content',I):
                                        D=A.message.extensions[C]['messageId'];E=B.get_message_info(A.message.chatId,D).json[_B]['resourceUrl']
                                        with urlopen(E)as F:zip=F.read();G=upload_bubble(file=zip,comId=A.comId);B.apply_bubble(chatId=A.message.chatId,bubbleId=G,applyToAll=_A)
                        except Exception as H:print(H)
def reconsocketloop():
        while _A:cli.close();cli.start();sleep(120)
socketloop=threading.Thread(target=reconsocketloop,daemon=_A)
socketloop.start()
print('ready')
