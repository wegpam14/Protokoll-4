
  
  **Name**:  *Patrick Wegl*  
  **Datum:** *04.12.2018*  
  **Uhrzeit:** *8:00-10:30*  
  **Gruppe:** *3*  
  
   
    
 **Anwesend:** Sarah Vezonik, Alois Vollmaier, Patrick Wegl, Mercedes Wesonig, Matthias Winter,  
  **Abwesend:** Thomas Winter
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

#### Befehle
```make``` -> führt das MakeTool aus  
```make clean``` -> kann verwendet werden wenn "clean" im Makefile steht  
```./(Name der Datei).elf /.exe``` ->führt die Anwendung aus (nicht nur für das MakeTool, jedoch bei der verwendung sehr Hilfreich)  



### Touch  
Mit touch kann man den Zeitstempel von Dateien ändern, d.h. auf die aktuelle Zeit bringen. Falls noch keine Datei vorhanden ist, erzeugt touch eine neue leere Datei.    
    
Im Grunde läuft die Abbarbeitung eines Makefile's solange, solange kein Fehler auftritt. Falls doch ein Fehler auftritt wird die Abbarbeitung gestoppt. Dies kann speziell zu kritisch werden, wenn gerade ein Befehl ausgeführt wird. Um dieses Problem vorzubeugen, schreiben wir vor *rm* ein *-*. Dies führt dazu, dass auch bei einem Fehler, der Löschbefehl ausgeführt wird.  
********************************************************************************************************************************
## Übung mit dem make Tool  
### 1. Übung  
Aufgabe war es ein Programm zu schreiben, welches "Programm Start" ausgeben soll.  
**main.c:**  
```c
#include <stdio.h>

int main(){
        printf("Programm start\n");
        return 0;
}  
```   
**Makefile**  


```ruby
ue04.elf: main.o monitor.o lcd.o
        gcc -o ue04.elf main.o monitor.o lcd.o  

main.o: main.c monitor.h lcd.h
        gcc -c main.c
        
        
monitor.o: monitor.c lcd.h
        gcc -c monitor.c
        
lcd.o: lcd.c
        gcc -c lcd.c
        
clean: 
        rm *.o
        rm *.elf
```

Mit "gcc" findet die Kompilierung der Dateien statt.  
Es werden Objektdateien wie z.B **main.o** aus **main.c** erstellt.
   

  

 
