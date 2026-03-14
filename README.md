# LAB-5-Reverse-Engineering-de-UnCrackable-Level-2

## 📌 Description
[cite_start]Ce laboratoire consiste à analyser l'application Android **Uncrackable Level 2** afin de découvrir le mot secret utilisé pour la validation[cite: 1]. [cite_start]L'objectif est de pratiquer le reverse engineering sur du code Java et du code natif compilé[cite: 1].

---

## 🛠️ Outils Utilisés
* [cite_start]**unzip** : Pour extraire le contenu du fichier APK[cite: 2, 3].
* [cite_start]**JADX** : Pour décompiler et analyser le code Java et le manifeste[cite: 12, 78].
* [cite_start]**Ghidra** : Pour le reverse engineering de la bibliothèque native `libfoo.so`.

---

## 📂 Étape 1 : Extraction et Analyse de la Structure
[cite_start]La première étape consiste à extraire l'APK pour accéder aux fichiers internes[cite: 2].
* [cite_start]**Commande** : `unzip UnCrackable-Level2.apk -d uncrackable_12`[cite: 3].
![image.png](attachment:f9678413-3c91-42ba-8529-91360ca5a21e:image.png)
* [cite_start]**Fichiers obtenus** : `AndroidManifest.xml`, `classes.dex`, et le répertoire `lib`[cite: 5, 112, 100].

> **🖼️ Image 1 : Structure des fichiers extraits**
> *(Capture d'écran montrant les fichiers AndroidManifest, classes.dex et le dossier lib)*

---

## 🔎 Étape 2 : Analyse du AndroidManifest.xml
[cite_start]Le manifeste révèle les informations de configuration de l'application[cite: 25].
* [cite_start]**Package** : `owasp.mstg.uncrackable2`[cite: 32].
* [cite_start]**Activité principale** : `sg.vantagepoint.uncrackable2.MainActivity`[cite: 44].

---

## 🧠 Étape 3 : Analyse du Code Java (JADX)
[cite_start]En analysant la `MainActivity`, on identifie la méthode de vérification[cite: 53].
* [cite_start]La fonction `verify` récupère le texte saisi et appelle la méthode `a` de la classe `CodeCheck`[cite: 55, 56].
* [cite_start]La classe `CodeCheck` contient une méthode **native** nommée `bar`[cite: 78, 80].
* [cite_start]Le code charge la bibliothèque native via `System.loadLibrary("foo")`[cite: 142].

```java
// Extrait de CodeCheck.java [cite: 80, 84]
private native boolean bar(byte[] bArr);

public boolean a(String str) {
    return bar(str.getBytes());
}
