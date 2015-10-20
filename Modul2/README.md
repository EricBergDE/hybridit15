# Modul 2 - Hybrid IT
## Agenda
* Virtuelle Netzwerke
* VPN-Verbindungen
* Azure Automation
* Azure Active Directory

## Demo
1. Virtuelles Netzwerk einrichten (ASM)
2. Point-to-Site (P2S) einrichten (ASM)
3. Automatisierung für Server on- und off-prem
4. Azure AD einrichten und App konfigurieren

## Hands-On
Alle Übungen können frei gewählt werden, da keine Abhängigkeiten zu anderen Modulen bestehen.

Empfohlene Kombinationen, die zeitlich in den Praxisteil passen:
1. Virtuelles Netzwerk einrichten (Ü1), P2S einrichten (Ü2) und ggf. Web-Server erstellen (Ü5)
2. Automatisierung für Server on- und off-prem (Ü3)
3. Extra-Übung: Azure Active Directory einrichten und App konfigurieren (Ü4)

### Ü1: Virtuelles Netzwerk einrichten (ASM)
Fakultativ. Empfohlen.

Im aktuellen Verwaltungsportal (ASM) ein neues virtuelles Netzwerk erstellen.

* Der Name kann frei gewählt werden.
* Die Region kann auch frei gewählt werden.

*Hinweis:*
Die Verwendung virtueller Netzwerke über den Azure Ressource Manager 
wären theoretisch auch möglich. Allerdings unterstützt das neue Portal derzeit 
nicht die Erstellung von P2S-Verbindungen, so dass die Konfiguration über 
PowerShell notwendig wäre.

### Ü2: Point-to-Site (P2S) einrichten (ASM)
Fakultativ. Zeitaufwand ca. 15min.  
Benötigt ein eingerichtetes virtuelles Netzwerk über ASM. (Vorherige Übung.)

1. P2S für ein virtuelles Netzwerk konfigurieren.
	* Aktivieren
	* Adressbereich für Client definieren
	* Gateway-Subnetz hinzufügen
1. Root- und Client-Zertifikate erstellen.
2. Öffentlichen Teil des Root-Zertifikats für das virtuelle Netzwerk zu Azure hochladen.
3. Client-Zertifikat (inkl. privatem Schlüssel) auf einem Client installieren.
	* Dies kann zu Test-Zwecken eine Test-VM sein, die eventuell im ersten Modul
	bereits erstellt haben.
4. VPN-Profil auf dem Client installieren.
5. Per P2S (VPN) mit dem virtuellen Netzwerk verbinden.
6. Optional: erhaltene VPN-Client-IP-Adresse überprüfen.

Es kann ein vorgefertiges Test-Zertifikat verwendet werden oder mit makecert 
eigene Zertifikate erstellen. 
* Erfordert makecert, welches auf den Teilnehmer-Laptops vorinstalliert ist.
* makecert ist u.a. Bestandteil von Visual Studio oder den Windows SDKs.

**Befehlszeilen für makezert:**  
Stammzertifikat  
makecert -sky exchange -r -n "CN=IT Camp Hybrid IT - P2S-Root" -pe -a sha1 -len 2048 -ss My

Client-Zertifikat  
makecert.exe -n "CN=IT Camp Hybrid IT - Client" -pe -sky exchange -m 96 -ss My -in "IT Camp Hybrid IT - P2S-Root" -is my -a sha1

### Ü3: Automatisierung für Server on- und off-prem
Fakultativ. Diese Übung ist etwas zeitaufwändiger, ca. 20min einplanen.

Grundlegende Schritte zu Wiederholung:  
1. Erstellen eines Azure Automation-Kontos
2. Erstellen eines einfachen PowerShell-Skriptes (Beispiel link hier)
3. Installation und Registrierung des Hybrid Worker auf einer beliebigen Windows-VM
4. Ausführen eines Skripts auf dem Hybrid Worker

### Ü4: Extra-Übung: Azure Active Directory einrichten und App konfigurieren
Fakultativ. Diese Übung ist etwas zeitaufwändiger, ca. 20min einplanen.

1. Ein neues Azure Active Directory (AAD) erstellen.
2. Ein neues Test-Benutzerkonto im neuen AAD erstellen.
3. Eine neue Anwendung im neuen AAD erstellen.
4. Mit dem neuen Test-Benutzer (aus Schritt 2) bei der neuen Anwendung (aus Schritt 3) 
	anmelden.
	* Einige Anwendungen, die in der Gallerie vom AAD zur Verfügung stehen, 
	unterstützen noch keine direkte Integration mit AAD. In solchem Fällen 
	ist die Installation eines Browser-Plug-Ins für den jeweiligen Browser 
	(verfügbar für Internet Explorer, Firefox oder Chrome) notwendig.

### Ü5: Extra-Übung: Web-Server im neuen VNet erstellen
Fakultativ. Diese Übung setzt die ersten beiden Übungen in diesem Modul voraus. 
D.h. ein virtuelles Netzwerk und eine P2S-Verbindung müssen eingerichtet sein.

1. Eine neue virtuelle Maschine im neu erstellten virtuellen Netzwerk erstellen.
	* Keine besonderen Ports für Web für die VM konfigurieren. Der Zugriff 
	soll später per P2S (VPN) erfolgen.
2. Bei einer Windows Server-VM die Web Server-Rolle installieren.
	* Lokal auf der VM prüfen, dass die Startseite vom IIS aufgerufen werden kann. 
	(http://localhost/)
4. Von der VM aus der zweiten Übung in das virtuelle Netzwerk per P2S verbinden.
5. Von der VM aus der zweiten Übung im Browser die Startseite des Web-Servers 
	aus Schritt 2 öffnen. 

## Weiterführende Links

[Virtuelle Netzwerke Übersicht](https://azure.microsoft.com/de-de/services/virtual-network/)  
[Virtuelle Netzwerke Dokumentation](https://azure.microsoft.com/de-de/documentation/services/virtual-network/)  
[Virtuelle Netzwerke Preise](https://azure.microsoft.com/de-de/pricing/details/virtual-network/)

[Azure Automation Übersicht](https://azure.microsoft.com/de-de/services/automation/)  
[Azure Automation Dokumentation](https://azure.microsoft.com/de-de/documentation/services/automation/)  
[Azure Automation Preise](https://azure.microsoft.com/de-de/pricing/details/automation/)

[Azure Active Directory Übersicht](https://azure.microsoft.com/de-de/services/active-directory/)  
[Azure Active Directory Dokumentation](https://azure.microsoft.com/de-de/documentation/services/active-directory/)  
[Azure Active Directory Preise](https://azure.microsoft.com/de-de/pricing/details/active-directory/)

[Azure Resource Explorer (Preview)](https://resources.azure.com/)

[Kurs "Das eigene Test Lab für jeden – mit IaaS von Microsoft Azure" in der Microsoft Virtual Academy](https://www.microsoftvirtualacademy.com/de-de/training-courses/das-eigene-test-lab-fr-jeden-mit-iaas-von-microsoft-azure-11743?l=2IEWUkkEB_6604984382)

[Vortrag Hybrid Automation & Identity mit Microsoft Azure von der ShareDev Cologne 2015 (auf Channel 9)](https://channel9.msdn.com/Events/community-germany/ShareDev-Cologne-2015/Hybrid-Automation--Identity-mit-Microsoft-Azure)

## Abkürzungen

AAD: Azure Active Directory  
ASM: Azure Service Management  
P2S: Point-to-Site  
VNet: Virtuelles Netzwerk