### LAB 5 : Reverse Engineering de UnCrackable Level 2
## unzip le fichier .apk 
j'utilise Gitbash

![Extraction APK](pic/unzip.png)

## Analyse du Manifeste et du Code Java

L'analyse du fichier AndroidManifest.xml permet d'identifier le point d'entrée de l'application

![Extraction APK](pic/manifest.png)

Dans la classe MainActivity, la fonction verify récupère le texte saisi par l'utilisateur et appelle this.m.a(string)

![Extraction APK](pic/verifie.png)

La classe CodeCheck (nommée m dans le code obfusqué) déclare une méthode native : private native boolean bar(byte[] bArr); . L'application charge la bibliothèque libfoo.so.

![Extraction APK](pic/checker.png)

## unzip unckrackabel L2:

Puisque la validation est "native", nous devons utiliser Ghidra pour transformer le code machine de libfoo.so en pseudo-code C lisible.

![Extraction APK](pic/fichier.png)

## Fichier .so:

![Extraction APK](pic/libfoo.png)

## lib foo:

Il n'est pas possible de visualiser ou d'analyser le contenu du fichier .so directement avec JAD
X
![Extraction APK](pic/satic.png)

![Extraction APK](pic/libfoo2.png)

car il s'agit d'une bibliothèque native compilée. Pour analyser ce type de fichier, il est nécessaire d'utiliser un outil de reverse engineering comme Ghidra.
## outil GHIDRA:

Outil : Utilisation de ghidraRun.bat pour lancer l'environnement d'analyse

![Extraction APK](pic/ghidra.png)

## ghidra lifoo file :

On peut visualiser et analyser le fichier .so à l'aide de Ghidra.

![Extraction APK](pic/libfooghidra.png)

## Identification du Secret

![Extraction APK](pic/source.png)

le code source c'est : Thanks for all the fish

