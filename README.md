# 1. Généralités
J'ai un disque dur de 10Go que je vais partitioner en deux avec :
  * Partion 1 de 6Go
    Elle sera de type ext4 et sera monté sur le dossier (qui devra être créer) /mnt/data.
  * Partion 2 de 4Go
    Elle sera de type SWAP, il faudra penser à désactiver le disque SWAP actuel qui est sur le disque sda5.

# 2. Partition sdb1
## Step 1 : Vérifier l'état des disques présents
![step1](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/0_lsblk.png)
## Step 2 : Avoir plus de données sur les disques présents
![step2](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/1_fdisk-l.png)
## Step 3 : Partionnement du disque sdb pour avoir notre disque sdb1 de 6Go sur plusieurs étapes avec la commande cfdisk /dev/sdb
Je choisis le type d'étiquette (dos)  
![step3-1](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/2-0_cfdisk-sdB.png)  
Je choisis l'espace libre et je vais sur "Nouvelle"  
![step3-2](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/2-1_cfdisk-sdB.png)  
Je spécifie la taille du partionnement à 6Go  
![step3-3](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/2-2_cfdisk-sdB.png)  
Je spécifie que la partition sera "primaire"  
![step3-4](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/2-3_cfdisk-sdB.png)  
La partion est prête, il faut maintenant "Ecrire" pour éviter de tout perdre  
![step3-5](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/2-4_cfdisk-sdB.png)  
## Step 4 : Vérification du partitionnement avec la commande fdsik -l
![step4](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/3_fdisk-l.png)
## Step 5 : Création du dossier mnt/data puis formatage au format ext4 et montage du disque sur /mnt/data
![step5](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/4_mkfs%26mount-sdb1.png)
## Step 6 : Modification du fichier fstab pour garder le montage au montage
![step6](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/5_fstab-sdb1.png)
## Step 7 : Vérification que le disque est bien monté sur /mnt/data après reboot de la machine
![step7](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/6_reboot-sdb1.png)

# 3. Partition sdb2
## Step 1 : Vérification de l'état des disques présets après partionnement du sdb2
![step1](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/7_lsblk-fdisk(rappel).png)
## Step 2 : Partionnement du disque sdb pour avoir notre disque sdb2 de 4Go sur plusieurs étapes avec la commande cfdisk /dev/sdb
> Attention, étant donnée que le disque sdb a déjà été partitionner pas besoin de choisir à nouveau le type d'étiquette car nous sommes déjà en dos  

Je choisis l'espace libre et je vais sur "Nouvelle"  
![step2-1](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/8-0_cfdisk-sdB.png)  
Je spécifie la taille du partionnement à 4Go  
![step2-2](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/8-1_cfdisk-sdB.png)  
Je spécifie que la partition sera "primaire"  
![step2-3](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/8-2_cfdisk-sdB.png)  
La partion est prête, il faut maintenant "Ecrire" pour éviter de tout perdre  
![step2-4](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/8-3_cfdisk-sdB.png)  
## Step 3 : Vérification du partitionnement avec la commande fdsik -l
![step3](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/9_fdisk-l.png)
## Step 4 : Eteindre le swap du disque sda5
![step4](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/10_swapOffsdA5.png)
## Step 5 : Formatage au format swap et démarrer sdb2 en swap
![step5](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/11_mkswap%26swapOnsdB2.png)
## Step 6 : Modification du fichier fstab pour garder le swapof du sda5 et le swapon du sdb2 au démarrage
![step6](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/12_fstab-sdb2.png)

# 4. Finalités
Après redémarrage, j'ai refait la commande lsblk pour m'assurer que toutes les modifications ont été sauvegardés :  
![final](https://github.com/Mirhazka/GestionStockageLinux/blob/main/Ressource/13_reboot-sdb2.png)
