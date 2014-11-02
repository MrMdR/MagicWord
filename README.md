Magicword
=========

Your sparkcore reads Twitter and execute an if/else statement when a matching word has been found!
(acctually... ThingSpeak reads twitter and gives your spark core a kick to do something...)

Make your spark core react to (almost) EVERYTHING with https://ifttt.com and the use of twitter!!

How To (NL)
=========
Instaleer en configureer je spark core en node.JS  <br>
https://community.spark.io/t/tutorial-spark-cli-on-windows-01-oct-2014/3112 <br>

Upload blink en voeg “Serial.println("Hi there! It works");” toe om te kijken of je seriele monitor alles goed ontvangt.   <hr>
Heb een twitter account. <br>
<h>
Maak een accound aan op www.thingsspeak.com <br>

Maak een channel aan onder channels > my channel  in het menu <br>
Geef het de naam “Magic word channel” <br>
enige wat je daar moet doen is dat Make public boxje aanvinken <br>

Maak een nieuwe ThingHttp aan onder ‘apps’ in het menu <br>
Name: “MagicWordToSpark” <br>
URL: https://api.spark.io/v1/devices/Jou-spark-Core-ID-NummeR/magicword <br>
Method: POST <br>
Host: api.spark.io <br>
Body: access_token=Jou-access-tokeN&magicword=%%trigger%% <br>

Jou-spark-Core-ID-NummeR vervangen door je CoreID.  <br>
Zoek je sparkcore ID (het nummer):  https://www.spark.io/build/ > cores <br>

Jou-access-tokeN moet je vervangen door je acces token. Zoek je spark access token:  https://www.spark.io/build/ > settings <br>

Maak een nieuwe ThingHttp aan onder ‘apps’ in het menu <br>
name: MagicWordFromTwitter <br>
url: http://api.thingspeak.com/update <br>
Method: POST <br>
Body: api_key=WRITE_KEY&field1=%%trigger%%&status=%%status%% <br>

WRITE_KEY moet je vervangen door de write api key van je channel die je aan het begin heb aangemaakt <br>
Deze is te vinden onder  (open een nieuw tablad > ) Chanels (menu) > my channels > “Magic word channel” > api key <br>

Maak een TweetControl aan: apps > tweetcontroll > “new tweetcontrol” <br>
Twitter Account: Jou_twitter_accounT <br>
Trigger: happycookie <br>
ThingHTTP Action: MagicWordFromTwitter <br>

Maak nu nog een TweetControl aan maar nu met het woord “sadcookie”. <br>

dan naar channels > my channel > private view <br>
daar zou je rechts '0 entries' moeten zien staan onder 'channel stats' <br>

Ga naar je twitter account <br>
Tweet: Tingspeak happycookie <br>
hashtags, hoofdletters en andere woorden negeert tie; deze kan je je dus bijvoegen maar hoeft niet. <br>

Minuutje wachten, channel pagina freshen en dan zou er "1 entry" moeten staan. <br>
Ja? Ga door! <br>
Nee? Iets niet goed gedaan… <br>
 <hr>
Kopieer de code naar https://www.spark.io/build/ <br>
Verander het channel ID (in de code 17847) naar jou channel ID. <br>
Deze is te vinden bij  channels > my channels > MagicWordChannel > schannel settings. <br>

Flash (upload) de code <br>

Open de serial monitor door in de ‘node.js command prompt’  “spark serial monitor” te typen. Druk op ENTER.<br>

Wacht tot er verbinding is… <br>

Is het ledje nu aan? tweet: Tingspeak sadcookie <br>
uit? Tweet: thingspeak happycookie <br>

Het duurd een minuutje na je tweet voordat je spark de D7 led aan/uit zet. <br>
