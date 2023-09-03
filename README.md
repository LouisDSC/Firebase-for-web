![Firebase](https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Img.png)

# Firebase for Web | FirebaseUI FirebaseAuth Firestore
## Features
This programming workshop will allow you to discover the basics of Firebase and use them to create interactive web applications.

## What you will learn
- Authenticate users with [Firebase Authentication](https://firebase.google.com/docs/auth?hl=fr) ;
 and [FirebaseUI](https://firebase.google.com/docs/auth/web/firebaseui?hl=fr);
- Sync data using [Cloud Firestore](https://firebase.google.com/docs/firestore);
- Write [Firebase](https://firebase.google.com/).

## What you'll need
- A browser of your choice, such as Chrome ;
- Access to [stackblitz](http://stackblitz.com/) (no account or sign-in necessary);
- A Google account, like a gmail account. We recommend the email account that you already use for your GitHub account. This allows you to use advanced features in StackBlitz;
- The codelab's sample code. See the next step for how to get the code.

## Get started now !
1. Noted that in this codelab, you build an app using [stackblitz](http://stackblitz.com/), an online editor that has several Firebase workflows integrated into it. Stackblitz requires no software installation or special StackBlitz account.
2. Go to [this URL](https://stackblitz.com/edit/firebase-gtk-web-start).
3. You can modify the file `index.html` as you see fit while leaving the ID and class untouched.
4. Create a Firebase project
   - Sign in to [Firebase](https://firebase.google.com/)
   - In the Firebase console, click Add Project (or Create a project), then name your Firebase project  Codelab-for-firebase-web like [this] (https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Create_project.png)
   - On the Google Analytics screen, click "Don't Enable", because you won't be using Analytics for this app.
   - If you want to know more about firebase projects, I advise you to read the [documentation](https://firebase.google.com/docs/projects/learn-more?hl=fr) before continuing.

## Enable and set up Firebase products in the console !
1. Firebase Authentication and Firebase UI to easily allow your users to sign in to your app.
To allow users to sign in to the web app, you'll use the Email/Password sign-in method for this codelab:
   - In the left-side panel of the Firebase console, click Build > Authentication. Then click Get Started. You're now in the Authentication dashboard, where you can see signed-up users, configure sign-in providers, and manage settings like this
   [this] (https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Create_project.png)
   [this] (https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Auth.png)
   [this] (https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Mail.png)
   - Select the Sign-in method tab and then click Email/Password from the provider options, toggle the switch to Enable, and then click Save.
   [this] (https://github.com/LouisDSC/Firebase-pour-le_web/blob/main/Img/Mail.png)

2. Set up Cloud Firestore



```json
"phpmailer/phpmailer": "^6.5"
```

ou si vous utilisez NPM & NodeJs :

```npm
composer require phpmailer/phpmailer
```

Dans le dossier `vendor`, le fichier script `vendor/autoload.php` est automatiquement généré par <i>Composer</i> et ne fait pas partir PHPMailer.

Si vous souhaitez utiliser la classe d'authentification Gmail XOAUTH2, vous devrez également ajouter une dépendance au`league/oauth2-client` package dans votre fichie `composer.json`.

AUssi, si vous n'utilisez pas Composer, vous pouvez [télécharger PHPMailer sous forme de fichier zip | ou le cloner](https://github.com/LouisDSC/PHPMailer), puis copiez le contenu du dossier PHPMailer dans l'un des `include_path` répertoires spécifiés dans votre Configuration PHP et chargez chaque fichier de classe manuellement :

```php
<?php
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\Exception;

require 'path/to/PHPMailer/src/Exception.php';
require 'path/to/PHPMailer/src/PHPMailer.php';
require 'path/to/PHPMailer/src/SMTP.php';
```

Même si vous n'utilisez pas la classe `SMTP`, vous devez toujours charger la classe `Exception` car elle est utilisée en interne.
### Installation importante !
Bien que l'installation de l'ensemble du package manuellement ou avec Composer soit simple, pratique et fiable, vous souhaiterez peut-être n'inclure que les fichiers vitaux dans votre projet. Au minimum, vous aurez besoin de [src/PHPMailer.php](https://github.com/LouisDSC/PHPMailer/blob/master/src/PHPMailer.php). 
- Si vous utilisez SMTP, vous aurez besoin de [src/SMTP.php](https://github.com/LouisDSC/PHPMailer/blob/master/src/SMTP.php).
 -Si vous utilisez POP avant SMTP ( très peu probable !), vous aurez besoin de[src/POP3.php](https://github.com/LouisDSC/PHPMailer/blob/master/src/POP3.php).
 - Si vous utilisez XOAUTH2, vous aurez besoin de [src/OAuth.php](https://github.com/LouisDSC/PHPMailer/blob/master/src/OAuth.php) ainsi que des dépendances Composer pour les services avec lesquels vous souhaitez vous authentifier. Vraiment, c'est beaucoup plus simple d'utiliser Composer ! Je vous le conseil vivement !

## Exemple que vous pouvez utiliser

```php
<?php
//Importer les classes PHPMailer dans l'espace de noms global 
//Celles-ci doivent être en haut de votre script, pas à l'intérieur d'une fonction 
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;

//Le chargeur automatique de Load Composer 
require 'vendor/autoload.php';

//Créer une instance ; passer `true` active les exceptions 
$mail = new PHPMailer(true);

try {
    //Paramètres du serveur
    $mail->SMTPDebug = SMTP::DEBUG_SERVER;                      // Activer la sortie de débogage détaillée
    $mail->isSMTP();                                            // Envoi via SMTP
    $mail->Host       = 'smtp.example.com';                     //Définir le serveur SMTP pour envoyer via
    $mail->SMTPAuth   = true;                                   //Activer l'authentification SMTP 
    $mail->Username   = 'user@example.com';                     //nom d'utilisateur SMTP 
    $mail->Password   = 'secret';                               // Mot de passe SMTP
    $mail->SMTPSecure = PHPMailer::ENCRYPTION_SMTPS;            //Activer le chiffrement TLS implicite 
    $mail->Port       = 465;                                    //Port TCP auquel se connecter ; utilisez 587 si vous avez défini `SMTPSecure = PHPMailer::ENCRYPTION_STARTTLS`

    //Destinataires
    $mail->setFrom('from@example.com', 'Mailer');
    $mail->addAddress('louis@example.net', 'Louis Japheth Kouassi');     //Ajouter un destinataire
    $mail->addAddress('japheth@example.com');               //Le nom est facultatif
    $mail->addReplyTo('info@example.com', 'Information');
    $mail->addCC('cc@example.com');
    $mail->addBCC('bcc@example.com');

     //Pièces jointes 
    $mail->addAttachment('/var/tmp/file.tar.gz');         //Ajouter des pièces jointes
    $mail->addAttachment('/tmp/image.jpg', 'new.jpg');    //Le nom est facultatif

    //Contenu
    $mail->isHTML(true);                                  // Définissez le format de l'e-mail sur HTML
    $mail->Subject = 'Sujet';
    $mail->Body    = 'Ceci est le corps du message HTML <b>en gras !</b>';
    $mail->AltBody = 'Ceci est le corps en texte brut pour les clients de messagerie non-HTML';

    $mail->send();
    echo 'Votre message a bien été envoyé';
} catch (Exception $e) {
    echo "Votre message n'a pas pu être envoyé. Erreur Mailer : {$mail->ErrorInfo}";
}
```

## Langue Français
PHPMailer est par défaut en anglais, mais dans le dossier de langue , vous trouverez de nombreuses traductions pour les messages d'erreur PHPMailer que vous pourriez rencontrer. Pour spécifier une langue, vous devez indiquer à PHPMailer laquelle utiliser, comme ceci :

```php
//Pour charger la version français
$mail->setLanguage('fr', '/optional/path/to/language/directory/');
```

## Bonne chance !

