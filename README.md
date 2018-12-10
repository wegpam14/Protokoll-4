
  
  **Name**:  *Patrick Wegl*  
  **Datum:** *04.12.2018*  
  **Uhrzeit:** *8:00-10:30*  
  **Gruppe:** *3*  
  
   
    
 **Anwesend:** Sarah Vezonik, Alois Vollmaier, Patrick Wegl, Mercedes Wesonig, Matthias Winter, Thomas Winter  
  **Abwesend:** ---
***********************************************************************************************************************************


## Übersetzungsvorgang eines Programmes  
Im groben Sprachgebrauch versteht man unter _Compelieren_, das gesamte Übersetzen eines Programmes, jedoch ist das Compelieren nur ein Teil davon. Für die Gesamte Übersetzung eines Programmes benötigt man folgende Schritte:    

Name | Funktion      
------- | --------  
*1. Präprozessieren* | Hier wird das Programm(*main.c*) vorbereitet. d.h Eingabedaten werden bereitgestellt, Headerdateien hinzugefügt.   
*2. Compelieren* | In diesem Schritt wird aus dem preprozessierten Code ein Assemblercode erzeugt. Die Datei heißt nun *main.a*  
*3. Assemblieren* | Nun wird die *main.a*, welche in Assemblersprache geschrieben ist, in Maschinenbefehle übersetzt. Die Datei heißt nun *main.o*.  
*4. Linken* | Der Linker verbindet alle Programmteile und vereint sie zu einem ausführbaren Programm (*a.exe* für Windows oder *a.out* für Ubunto)  
*5. Umwandelen* | Hier wird die *a.out* oder *a.exe* in ein Format umgewandelt, das der Programmer versteht. z.B. Hex  
********************************************************************************************************************************  
  
## Übersezten mithife des make-Tools  
Mithilfe des make-Tools kann man den Übersetztungsvorgang steuern. Hierfür benötigt man ein *Makefile*.  
Weitere Informationen zum make Tool:  
[Wikipedia/make](https://de.wikipedia.org/wiki/Make)  
[Mikiwiki/make](http://mikiwiki.org/wiki/make)   
Der großer Vorteil ist, dass wenn man an einem Programmierprojekt arbeitet, nicht alle Dateien mit Partnern ausgetauscht werden müssen. Es reicht nämlich, wenn man die *main.c* und das dazupassende *Makefile* übermittelt. Die restlichen Dateien (main.o und Ausgabedatei) werden dann vor Ort am Rechner produziert werden. Dies vermindert die Datenübertragung und funktioniert auch immer, solange das *Makefile* gleich bleibt.  


### Makefile  
Ein Makefile wird mithilfe eines Texteditors geschrieben, worin die Information für das make Tool stehen. Es werden Ziele(targets), Abhängigkeiten(dependencis) und Kommandos(Commands) benötigt. In der Folgenden Grafik soll dies veranschaulicht werden.  
```
Ziel A: Abhängigkeiten  
*tab* Kommando 1  
*tab* Kommando 2   
*tab* Kommando 3 ...  
  
Ziel B: Abhängigkeiten  
*tab* Kommando 1  
*tab* Kommando 2  
*tab* Kommando 3 ...   
```  
Bei *tab* ist sehr sehr wichtig, dass man einen echten Tabulator verwendet und dass man zwischen die Zielen eine Leerzeile einfügt. Ansonsten funktioniert das gesamte make Tool nicht.  

### make im Terminal  
Tippt man das **make** im Terminal ein, sucht es sich selbstständig, ob die angegebenen Zieler erreicht werden können. Weiters schaut es auch ob alle Dateien auf den neuesten Stand sind. Angenommen falls die *main.c* einen jüngeren Zeistempel als die *main.o* hat, dann wird alles neu compeliert und gelinkt. Falls man die Zeitstempel nahträglich ändern will, kann man dies mit *touch* tun.  
#### Touch  
Mit touch kann man den Zeitstempel von Dateien ändern, d.h. auf die aktuelle Zeit bringen. Falls noch keine Datei vorhanden ist, erzeugt touch eine neue leere Datei.    
    
Im Grunde läuft die Abbarbeitung eines Makefile's solange, solange kein Fehler auftritt. Falls doch ein Fehler auftritt wird die Abbarbeitung gestoppt. Dies kann speziell zu kritisch werden, wenn gerade ein Befehl ausgeführt wird. Um dieses Problem vorzubeugen, schreiben wir vor *rm* ein *-*. Dies führt dazu, dass auch bei einem Fehler, der Löschbefehl ausgeführt wird.  
********************************************************************************************************************************
## Übung mit dem make Tool  
### 1. Übung  
Mithilfe des nano Editor und des make Tools, sollt "Guten Morgen" am Terminal ausgegeben werden.  
**main.c:**  
```c
#include <stdio.h>

int main(){
        printf("Guten Morgen\n");
        return 0;
}  
```   
**Makefile**  
```  
# Hallo, das ist ein Kommentar

test1: main.o
        gcc -otest1 main.o

main.o: main.c
        gcc -c main.c

cleanAndBuild: clean test1

clean:
        -rm main.o
        -rm test1
```  

Nun kann man mittles dem *make* Befehl im Terminal, die Abarbeitung starten.    

Befehl | Beschreibung  
------ | ------------    
make clean | Alle, von *make* erstellten Dateien, werden gelöscht.   
make cleanAndBuild |  Alle, von *make* erstellten Dateien, werden gelöscht und danach wieder erstellt.
make main.o | Der Programmiercode wird in Maschinenbefehlt übersetzt.  
  
### 2.Übung  
Ein C-Programm für den Arduino Nano schreiben, das die LED blinken lässt. Hierfür werden mehrere Dateien benötigt, die man dann alle richtig im Makeflie abhängig machen muss.  
**main.c**  
```  
 
