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
<img width="1637" height="911" alt="Screenshot_2026-03-30_07-43-45" src="https://github.com/user-attachments/assets/587aa743-8c9b-4a88-ada9-9e246110cc5f" />
<img width="1920" height="431" alt="image" src="https://github.com/user-attachments/assets/9c5a3c69-af83-45fd-8f5b-f3d00178620b" />
Description : 
Cette étape consiste à examiner le fichier AndroidManifest.xml de l’application et les permissions demandées. L’objectif est d’identifier les configurations sensibles comme android:debuggable, android:allowBackup ou android:usesCleartextTraffic, ainsi que les permissions dangereuses et les composants exportés. Cette analyse permet de repérer des failles potentielles liées aux accès aux données et à la sécurité globale de l’application.

Task 5 — Analyse de la configuration réseau :









