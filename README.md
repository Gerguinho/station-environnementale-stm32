# Station DEEP — Station de mesure environnementale sur STM32

Système embarqué en C qui mesure en temps réel la température, l'humidité, la pression, l'altitude, la luminosité et la proximité. Les mesures s'affichent sur un écran TFT, et la station déclenche des alertes visuelles et sonores quand l'humidité sort des seuils réglés.

**Matériel :** STM32G431KB (Nucleo-G431KB) · DHT11 · BMP180 · APDS9960 · écran TFT ILI9341 · LED · buzzer
**Outils :** C · STM32 HAL · STM32CubeIDE

## Fonctionnalités

- **Mesures** : température et humidité (DHT11), pression et altitude (BMP180), luminosité ambiante et proximité (APDS9960).
- **Affichage** : écran d'accueil, puis tableau de bord sur l'écran ILI9341.
- **Alertes d'humidité** : une LED pour le seuil haut (PB4), une pour le seuil bas (PB5), et un bip intermittent du buzzer (PA11). Le bip est cadencé sans bloquer la boucle principale.
- **Réglage des seuils** : le bouton PA0 permet de passer en mode configuration et de modifier les seuils min/max (30 % et 70 % par défaut).
- **Mise en veille automatique** : la station se met en veille après 10 s d'obscurité et se réveille dès que la lumière revient.

## Organisation du code

```
app/
  main.c        Boucle principale : capteurs, bouton, veille, alertes, affichage
  config.h      Broches et activation des modules (écran, polices, UART…)
core/           Démarrage, interruptions, script d'édition de liens (STM32G431KB)
drivers/
  bsp/          Pilotes des capteurs et périphériques (DHT11, BMP180, APDS9960, ILI9341…)
  stm32g4xx_hal Bibliothèque HAL de ST
  cmsis/        Couche CMSIS
```

Le développement a été organisé en branches de fonctionnalités (`feature-driver-adc`, `feature-gestion-pwm`, `feature-demo-rapport`), fusionnées dans `main`.

## Compiler et flasher

1. Ouvrez le dossier dans **STM32CubeIDE** (*File → Import → Existing Projects into Workspace*).
2. Compilez avec la configuration **Debug**.
3. Branchez la carte Nucleo-G431KB en USB, puis lancez *Run* ou *Debug*.

## Équipe

Projet réalisé en binôme par **Monthe Youmbi Yvan Fabrice** et **Bryan Hounang Petcheu** ([GitHub](https://github.com/Gerguinho)).
