Magicword
=========

Your sparkcore reads Twitter and execute an if/else statement when a matching word has been found!


How To (NL)
=========
Instaleer en configureer je spark core en node.JS 
https://community.spark.io/t/tutorial-spark-cli-on-windows-01-oct-2014/3112

Upload blink en voeg “Serial.println("Hi there! It works");” toe om te kijken of je seriele monitor alles goed ontvangt. 

Heb een twitter account aan.

Maak een accound aan op www.thingsspeak.com

Maak een channel aan onder channels > my channel  in het menu
Geef het de naam “Magic word channel”
enige wat je daar moet doen is dat Make public boxje aanvinken

Maak een nieuwe ThingHttp aan onder ‘apps’ in het menu
Name: “MagicWordToSpark”
URL: https://api.spark.io/v1/devices/Jou-spark-Core-ID-NummeR/magicword
Method: POST
Host: api.spark.io
Body: access_token=Jou-access-tokeN&magicword=%%trigger%%

Jou-spark-Core-ID-NummeR vervangen door je CoreID. 
Zoek je sparkcore ID (het nummer):  https://www.spark.io/build/ > cores

Jou-access-tokeN moet je vervangen door je acces token. Zoek je spark access token:  https://www.spark.io/build/ > settings

Maak een nieuwe ThingHttp aan onder ‘apps’ in het menu
name: MagicWordFromTwitter
url: http://api.thingspeak.com/update
Method: POST
Body: api_key=WRITE_KEY&field1=%%trigger%%&status=%%status%%

WRITE_KEY moet je vervangen door de write api key van je channel die je aan het begin heb aangemaakt
Deze is te vinden onder  (open een nieuw tablad > ) Chanels (menu) > my channels > “Magic word channel” > api key

Maak een TweetControl aan: apps > tweetcontroll > “new tweetcontrol”
Twitter Account: Jou_twitter_accounT
Trigger: happycookie
ThingHTTP Action: MagicWordFromTwitter

Maak nu nog een TweetControl aan maar nu met het woord “sadcookie”.

dan naar channels > my channel > private view
daar zou je rechts '0 entries' moeten zien staan onder 'channel stats'

Ga naar je twitter account
Tweet: Tingspeak happycookie
hashtags, hoofdletters en andere woorden negeert tie; deze kan je je dus bijvoegen maar hoeft niet. 

Minuutje wachten, channel pagina freshen en dan zou er "1 entry" moeten staan.
Ja? Ga door!
Nee? Iets niet goed gedaan…


Kopieer de code naar https://www.spark.io/build/
Verander het channel ID (in de code 17847) naar jou channel ID.
Deze is te vinden bij  channels > my channels > MagicWordChannel > schannel settings.

Flash (upload) de code

Open de serial monitor door in de ‘node.js command prompt’  “spark serial monitor” te typen. Druk op ENTER.

Wacht tot er verbinding is… 

Is het ledje nu aan? tweet: Tingspeak sadcookie
uit? Tweet: thingspeak happycookie

Het duurd een minuutje na je tweet voordat je spark de D7 led aan/uit zet.

