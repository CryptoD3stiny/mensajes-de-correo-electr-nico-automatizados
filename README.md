# mensajes-de-correo-electr-nico-automatizados
enviar mensajes de correo electrónico automatizados en Python

![image](https://github.com/user-attachments/assets/b81c2ad5-c9cf-405d-b9ca-9d4bac64ed41)


En este artículo, vamos a ver cómo enviar mensajes de correo electrónico automatizados que implican la entrega de mensajes de texto, fotos esenciales y archivos importantes, entre otras cosas. en Python.

Usaremos dos bibliotecas para esto: email y smtplib, así como el objeto MIMEMultipart. Este objeto tiene varias subclases; Estas subclases se utilizarán para crear nuestro mensaje de correo electrónico.

MIMEText: Consiste en un texto simple. Este será el cuerpo del correo electrónico.
MIMEImage: Esto nos permitiría agregar imágenes a nuestros correos electrónicos.
MIMEAudio: Si deseamos agregar archivos de audio, podemos hacerlo fácilmente con la ayuda de esta subclase.
MIMEAplica: Esto se puede usar para agregar cualquier cosa o cualquier otro archivo adjunto.
Implementación paso a paso
Paso 1: Importe los siguientes módulos:


from email.mime.text import MIMEText
from email.mime.image import MIMEImage
from email.mime.application import MIMEApplication
from email.mime.multipart import MIMEMultipart
import smtplib
import os


Paso 2: Configuremos una conexión a nuestro servidor de correo electrónico.

Proporcione la dirección del servidor y el número de puerto para iniciar nuestra conexión SMTP
Luego usaremos smtp. ehlo para enviar un comando EHLO (Extended Hello).
Ahora, usaremos smtp. starttls para habilitar el cifrado de seguridad de la capa de transporte (TLS).

smtp = smtplib.SMTP('smtp.gmail.com', 587)
smtp.ehlo()
smtp.starttls()
smtp.login('YourMail@gmail.com', 'Your Password')


Paso 3: Ahora, construya el contenido del mensaje.

Asigne el objeto MIMEMultipart a la variable msg después de inicializarla.
La función MIMEText se utilizará para adjuntar texto.

msg = MIMEMultipart()
msg['Subject'] = subject
msg.attach(MIMEText(text)) 


Paso 4: Veamos cómo adjuntar imágenes y varios archivos adjuntos.

Adjuntando imágenes:

Primero, lea la imagen como datos binarios.
Adjunte los datos de la imagen a MIMEMultipart usando MIMEImage, agregamos el nombre de archivo dado use os. Nombre de la base

img_data = open(one_img, 'rb').read()
msg.attach(MIMEImage(img_data, 
                     name=os.path.basename(one_img)))
Adjuntar varios archivos:

Lea en el archivo adjunto usando MIMEApplication.
A continuación, editamos los metadatos del archivo adjunto.
Finalmente, agregue el archivo adjunto a nuestro objeto de mensaje.

with open(one_attachment, 'rb') as f:
    file = MIMEApplication(
        f.read(), name=os.path.basename(one_attachment)
    )
    file['Content-Disposition'] = f'attachment; \
    filename="{os.path.basename(one_attachment)}"'
    msg.attach(file)

    
Paso 5: El último paso es enviar el correo electrónico.

Haz una lista de todos los correos electrónicos que quieres enviar.
A continuación, mediante la función sendmail, pase parámetros como desde dónde, hasta dónde y el contenido del mensaje.
Por último, simplemente salga de la conexión del servidor.

to = ["klm@gmail.com", "xyz@gmail.com", "abc@gmail.com"]
smtp.sendmail(from_addr="Your Login Email",
              to_addrs=to, msg=msg.as_string())
smtp.quit() 


Programar mensajes de correo electrónico
Para programar el correo, haremos uso del paquete schedule en python. Es muy ligero y fácil de usar.

Instalar el módulo

pip install schedule
Ahora observe las diferentes funciones que se definen en un módulo de programación y su uso:


La siguiente función llamará a la función mail cada 2 segundos.

schedule.every(2).seconds.do(mail) 


Esto llamará a la función mail cada 10 minutos.

schedule.every(10).minutes.do(mail)


Esto llamará a la función cada hora.

schedule.every().hour.do(mail)



Llamando todos los días a las 10:30 AM.

schedule.every().day.at("10:30").do(mail)
Llamando a un día en particular.

schedule.every().monday.do(mail)
