---
layout: post
title: "Installation nouveau disque dur"
tags: geekage
---

Le premeir disque dur de greyjot a rendu l'âme (Seagate 2TB). Remplacer par un Toshiba 3TB.
Tentative de sauvegarde des données.

## Formatage du nouveau disque

### Partitionnement

```
sudo cfdisk /dev/sda
```

Choix de 2 partitions de 1.2 et 1.5TB respectivement.

### Formatage des partitions

Espace réservé pour root petit (0.1), et flag largefile (inodes 1MB) compte-tenu du
stockage de fichiers relativement volumineux (photos, vidéos, musique).

```
sudo mkfs.ext4 -T largefile -m 0.1 /dev/sda1
sudo mkfs.ext4 -T largefile -m 0.1 /dev/sda2
```

### Points de montage

Edit /etc/fstab

```
/dev/sda1 /media/data ext4 defaults,noatime 0 1
/dev/sda2 /media/videos ext4 defaults,noatime 0 1
```

Puis

```
sudo mount -a
sudo chown -R nicolas:users /media/data
sudo chown -R nicolas:users /media/videos
```

Et ça devrait être bon...

## Récupération de l'ancien disque

A priori pas d'utilisation de `dd` vu que les partitions ont des tailles différentes.

```
cd /media
sudo mkdir tmp
sudo mount /dev/sdc1 tmp
cp -r tmp/SteamLibrary data
```
