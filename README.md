# LAB-6-Analyse-statique-d-un-APK-avec-MobSF-dans-la-VM-Mobexler

Task 1 — Préparation de l'environnement d'analyse : 
On crée un dossier de travail daté, on copie l’APK, et on note les informations essentielles pour la traçabilité : hash SHA-256, taille du fichier, date, analyste et version de la VM. Cette étape garantit la reproductibilité et la sécurité de l’audit.
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/dde17b91-7d45-49b5-9109-24cd3f39c477" />

Task 2 — Lancement de MobSF : 
MobSF est lancé dans la VM, et son interface web est vérifiée à l’adresse http://127.0.0.1:8000. La version de MobSF est notée pour la traçabilité. Cette étape prépare l’environnement pour l’analyse statique et dynamique de l’APK.
<img width="1640" height="991" alt="image" src="https://github.com/user-attachments/assets/11a6cb6b-e145-4cb2-b9e3-2491e1729cdf" /> 

Task 3 — Import et analyse de l'APK :
L’APK est importé dans MobSF via le bouton Upload & Analyze. MobSF effectue une analyse statique complète, générant un rapport détaillé avec le score de sécurité, les permissions, les composants et les vulnérabilités potentielles. L’heure de début et de fin, ainsi que le score, sont notés dans le fichier de traçabilité.
<img width="1637" height="911" alt="Screenshot_2026-03-30_07-43-45" src="https://github.com/user-attachments/assets/f5528a20-c32d-4175-a586-c2acbae2a81c" />

Task 4 — Analyse du manifeste et des permissions :
App Name : HelloWorld
Package Name : com.example.youngwind.helloworld
Main Activity : com.example.youngwind.helloworld.MainActivity
Target SDK 24 Min SDK 15 Max SDK
Android Version Name 1.0 Android Version Code 1 
Sur manifest analysis : 
Debug Enabled For App
[android:debuggable=true]  donc l’application peut être déboguée, ce qui peut exposer des données sensibles . 
Application Data can be Backed up
[android:allowBackup=true] 
<img width="1620" height="620" alt="image" src="https://github.com/user-attachments/assets/d54e448d-2ba5-427f-b2c9-8e64be2e8067" />
<img width="1919" height="902" alt="image" src="https://github.com/user-attachments/assets/7af479ba-5c80-4f98-bc6f-67aaa1332369" />
<img width="1348" height="766" alt="image" src="https://github.com/user-attachments/assets/51c1ebcb-35ad-4a1e-93a8-5ba1571191b1" />

Description : 
Cette étape consiste à examiner le fichier AndroidManifest.xml de l’application et les permissions demandées. L’objectif est d’identifier les configurations sensibles comme android:debuggable, android:allowBackup ou android:usesCleartextTraffic, ainsi que les permissions dangereuses et les composants exportés. Cette analyse permet de repérer des failles potentielles liées aux accès aux données et à la sécurité globale de l’application.L’analyse du manifeste de l’application Lab8 a révélé plusieurs problèmes de sécurité .
Premièrement, l’application peut être installée sur des versions anciennes d’Android (minSdk=26),  qui expose l’application à des vulnérabilités connues. 
Deuxièmement, l’option android:usesCleartextTraffic est activée, ce qui signifie que l’application autorise les communications non chiffrées (HTTP). Cela expose les données à des attaques de type Man-In-The-Middle (MITM).
Troisièmement, le mode debug est activé (android:debuggable=true), ce qui représente un risque critique, car un attaquant peut analyser et manipuler l’application plus facilement.
Enfin, la présence d’une configuration de sécurité réseau (networkSecurityConfig) est notée, mais elle doit être correctement configurée pour éviter les failles.
Ces éléments augmentent considérablement la surface d’attaque de l’application et doivent être corrigés avant un déploiement en production.
<img width="1345" height="758" alt="image" src="https://github.com/user-attachments/assets/642d3fbf-97b7-4081-b3b7-09773ff38643" />


Task 5 — Analyse de la configuration réseau :
<img width="518" height="111" alt="image" src="https://github.com/user-attachments/assets/4034e602-7c75-41d1-94ce-452d09008647" />
<img width="1338" height="287" alt="image" src="https://github.com/user-attachments/assets/a168e9db-c0b7-4036-810f-3061178e3a0a" />
Tout d’abord, la présence du paramètre cleartextTrafficPermitted indique que l’application autorise le trafic en clair via le protocole HTTP. Cela expose les communications à des attaques de type Man-In-The-Middle (MITM), permettant à un attaquant d’intercepter ou de modifier les données échangées.


Task 6 — Analyse du code et des ressources : 
Créer fichier vulnérabilités
Ajouter Hardcoded Secrets
Ajouter URLs / Emails 
Créer ressources sensibles
<img width="1729" height="925" alt="image" src="https://github.com/user-attachments/assets/3d5dc836-8df2-4083-8c05-4f3765b7b998" />


Task 7 — Corrélation avec OWASP MASVS : 
L’analyse montre que l’application présente deux principales non-conformités au standard OWASP MASVS : l’utilisation du trafic HTTP non sécurisé et l’emploi d’une adresse IP locale (10.0.2.2) inadaptée à la production. Ces failles exposent l’application à des risques comme les attaques Man-in-the-Middle et reflètent une mauvaise configuration réseau. Les tests du MASTG complètent l’évaluation en vérifiant notamment l’usage de HTTPS et le stockage sécurisé des données sensibles.

<img width="1729" height="103" alt="image" src="https://github.com/user-attachments/assets/d672d4be-a2ba-451a-b303-a192d7b2358f" />
<img width="1729" height="103" alt="image" src="https://github.com/user-attachments/assets/8c7cc634-cff3-45db-983d-1fe2e674022a" />



















