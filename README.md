# LAB17-Cracker-OWASP-Uncrackable-Android-Level-3

Étape 1 : Analyse statique simple avec Jadx-GUI (comprendre le Java)

verifyLibs() : vérifie CRC des .so et du DEX (via fonction native baz).

<img width="1907" height="771" alt="image" src="https://github.com/user-attachments/assets/b7a8a208-db78-4789-9f66-2c8af010c2e4" />


Si ça ne correspond pas → variable tampered = 31337.

onCreate() appelle showDialog() si root ou tampered → l’app quitte.

<img width="1920" height="975" alt="image" src="https://github.com/user-attachments/assets/7851d7c8-3b84-4ede-aac1-bf2e4c1bbc81" />


System.loadLibrary("foo") charge libfoo.so.

<img width="1920" height="968" alt="image" src="https://github.com/user-attachments/assets/32fa493c-0028-4f51-8b83-349757b1bca5" />

Étape 2 : Décompiler l’APK avec apktool (pour pouvoir modifier)

<img width="957" height="303" alt="image" src="https://github.com/user-attachments/assets/52c617fd-80c3-4f1f-b8bf-ef3eaf81f072" />

Étape 3 : Patch smali – Supprimer le message « tampered » / root

1. Dans l’explorateur de gauche de Vs code , va dans : smali → sg → vantagepoint → uncrackable3 → double-clic sur MainActivity.smali

2. Chercher le bloc d’erreur (Ctrl + F) -> showDialog

<img width="1791" height="1011" alt="image" src="https://github.com/user-attachments/assets/0579fe29-271f-4017-b6d4-7677d0873816" />

Résultat 1 → la méthode complète showDialog (qui crée le popup « This is unacceptable... »)

Résultat 2 → L’appel dans onCreate ← C’EST CELUI QUE NOUS ALLONS PATCHER

Résultat 3 → la méthode synthétique access$000

3. Le bloc exact à modifier (copie-colle)

<img width="918" height="717" alt="image" src="https://github.com/user-attachments/assets/56b784d3-ac67-4118-b48c-9afd4d7bbd63" />


<img width="532" height="817" alt="image" src="https://github.com/user-attachments/assets/ce48df68-7d02-4367-968c-3644300d722f" />

Étape 4 : Patch de la librairie native avec Ghidra (anti-debug + anti-Frida)

<img width="976" height="511" alt="image" src="https://github.com/user-attachments/assets/899a3aa7-1c9e-47d9-a7a3-8aba0fdfebe9" />






