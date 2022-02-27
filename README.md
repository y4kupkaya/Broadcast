<p><strong> <h1> 📢 <a
href="https://aylak-github/Broadcast"> Broadcast </a> </h1></strong></p>
</p>

<details>
  <summary><br> <h3> <b> 🧩 Özellikleri </b> </h3></br></summary>
   • Gruplar ve üyelere yayın yapabilir, </br> 
<br> • Toplam grup ve üye sayılarını görebilir,</br>
<br> • Kullanıcıları veya grupları botunuzun kullanımından yasaklayabilirsiniz. </br>
<br><br>
  <details><summary><br> <b> ➕ Ek özellikler </b></br></summary> 
    <p align="left">
    <br> • İsteğe bağlı gruplarda değiştirilebilir komut silme özelliği,</br>
<br> • Yasaklılar listesini görme özelliği,</br>
<br> • Yapılacak yayının iletimi yoksa kopyası olarak mı göndereliceğinin seçilebilir olması.</br>
</br>     
   </details>
</details>

<br>Broadcast'i kullanmak için bazı gereksinimler vardır.</br> 
<details>
  <summary><b> 📍 Gereksinimler </b></summary><br>
  <details>
    <br><summary><br> DATABASE_URL </br></summary>
    <p align="left">
    Veritabanı olarak MongoDB kullanıldığı için MongoDB url almanız gerekmektedir. Nasıl alınacağını bilmiyorsanız, <a href="https://t.me/LuciTools/12">burayı</a> kontrol edebilir ya da <a href="https://t.me/repohanex">destek grubuna</a> gelerek yardım alabilirsiniz.</br>
    </details><br>

  <details><summary><br> 🌀 BOT_USERNAME </br></summary> <br>
    <p align="left">
    <a href="https://t.me/botfather">@BotFather</a>'dan oluşturduğunuz botun kullanıcı adı.
    </details><br>

  <details><summary><br> 📋 LOG_CHANNEL</br></summary>
    <p align="left">
    <br> Botun eylemleri kaydedeceği grub'un kimliği. Kimliği elde etmek için, bir grup oluşturun ve <a href="https://t.me/missrose_bot">@MissRose_bot</a>'u gruba ekleyin ve <code>/id</code> yazın.</br>
    </details><br>

  <details><summary><br> 🔹 GROUP_SUPPORT</br></summary> 
    <p align="left">
    <br>Kullanıcıların itiraz edebilmesi için bir grup kimliği yazın. Eğer ayarlanmazsa, bot sahibine yönlendirir.</br>
    </details><br>

  <details><summary><br>OWNER_ID</br></summary>
    <p align="left">
    <br>Botun sahibinin id'si</br>
   </details><br>

<details><summary><br>😃 LANGUAGE</br></summary>
    <p align="left">
    <br>İki dil mevcuttur, Türkçe ve Azerbaycanca. Eğer ayarlanmazsa Türkçe olur.</br>
   </details><br>

<details><summary><br>♻️ GONDERME_TURU</br></summary>
    <p align="left">
    <br>Gönderilen mesajın ne şekilde gönderileceğini ayarlamak içindir. <code>False</code> olarak ayarlarsanız iletir, <code>True</code> olarak ayarlarsanız kopyasını gönderir.</br>
   </details><br>
</details>
<br>
<br><strong> <h3><b> 🧮 Kullanım </b></h3> </strong></br>
Botunuz, çok modüllü ise dosyaları arasına alıp gerekli değişkenleri yerel ya da sunucunun olarak ekledikten sonra <code>requirements.txt</code> dosyasına gerekli kütüphaneleri ekleyin. </br><br> Ama eğer tek dosya üzerinden çalışıyorsanız <code>Client</code>'i kendi botunuzun <code>Client</code>'ine göre değiştirmeniz gerekmektedir.</br><br></br>


<details>
  <summary><b> 📚 Gerekli kütüphaneler </b> </summary>

```toml
pymongo[srv]
aiofiles
psutil
```
</details>
</br>
<details>
  <summary><b> 💻 Ek olarak </b></summary><br>

Mesaj silme özelliği kodları:
<details>
  <summary><b> Komut mesajlarını silme özelliğini açmak isteyenler için kod: </b></summary><br>



```python
@Client.on_message(~filters.private)
async def delcmd(_, message: Message):
    if await delcmd_is_on(message.chat.id) and message.text.startwith("/") or message.text.startwith("!"):
        await message.delete()
    await message.continue_propagation()
```
</details>

<details>
  <summary><b> Mesaj silme özelliğinin farklı gruplarda kapatılıp açılmasını sağlayan kod: </b></summary><br>

```py
@Client.on_message(filters.command("delcmd") & ~filters.private)
async def delcmdc(bot: Client, message: Message):
    if len(message.command) != 2:
        return await message.reply_text("Bu komutu kullanmak için komutunuzun yanına 'off' ya da 'on' yazınız.")
    durum = message.text.split(None, 1)[1].strip()
    durum = durum.lower()
    chat_id = message.chat.id

    if durum == "on":
        if await delcmd_is_on(message.chat.id):
            return await message.reply_text("Komut Silme Zaten Açık.")
        else:
            await delcmd_on(chat_id)
            await message.reply_text("Bu sohbet için Komut Silme özelliği başarıyla etkinleştirildi.")

    elif durum == "off":
        await delcmd_off(chat_id)
        await message.reply_text("Bu Sohbet için Komut Silme özelliği başarıyla devre dışı bırakıldı.")
    else:
        await message.reply_text("Bu komutu kullanmak için komutunuzun yanına 'off' ya da 'on' yazınız.")
```
</details>
</details>