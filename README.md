# Protocole_COO_POO
Ici les fichiers temporaires pour le chat system en java.

## Les fichiers
La classe Message : permet d'échanger les différents types de données du chat system.

La class ControlMessage : correspond au message envoyé lors de l'initilisation de la connection,
du changement de statut (offline, online, away, connected, disconnected...).

## Protocole de communication
Le port a utiliser est le port : 15530 pour les communications de control.

Il faut ensuite crée une nopuvelle socket TCP (Socket ou ServerSocket) pour chaque nouvelle discussion,
cette socket doit être inititaliser avec un port (que vous choissisez). Cependant le port choisit 
doit être transmit à l'utilisateur pour lequel la socket à été ouverte.

Phase détablissement de connexion :
1. Envoie en brodcast d'un ControlMessage avec Data :"hello" lors de la connexion sur le chat.
2. Lors de la reception du message hello, vous devez créer une socket pour cette utilisateur et
répondre avec un ControlMessage contenant la data :"socket_created" et le port de la socket créee.
3. Lorsqu'un utilisateur reçoit un ControlMessage avec pour data "socket_created", il y a deux cas
possible : 
  - soit l'utilisateur possède déjà une socket chez vous, il suffit alors de sauvegarder le port reçu
  (ce sera celui-ci ou il faudra communiquer).
  - soit l'utilisateur n'a pas encore de socket chez vous, il faut lui en créer une et envoyer le port
  sur lequel cette socket à été créer (message socket_created et le port de la socket).
