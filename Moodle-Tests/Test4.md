## ACHTUNG! Die Reihenfolge der Multiple-Choice-Aufgabe ist zufällig!

#Frage 1

Welche ist die minimale Sichtbarkeit, die eine Methode haben muss, damit der Aufruf möglich ist?


#Frage 2

Welche Informationen enthält diese Grafik.

Ziehen Sie die Begriffe über entsprechenden Artefakte in der Grafik. Manche Begriffe müssen mehrfach verwendet werden. 

Beachten Sie bitte, dass das Fadenkreuz im Kreis (nicht der Text) die Position in der Grafik markiert. 



#Frage 3

ABSTRAKTION ist der Übergang von der Betrachtung einzelner individueller Objekte zu Klassen von Objekten mit gemeinsamen Eigenschaften.
MODULARISIERUNG ist das Zerlegen eines Problems in mehrere Teilprobleme.


#Frage 4

- [x] ```Joe
- [ ] ```Averell
- [ ] ```Keins von dem

#Frage 5

In dieser Aufgabe sollen Sie das Klassendesign der Uhren Aufgabe verändern.

Beim gegenwärtigen Design der Klasse ClockDisplay ist eine Instanz davon verantwortlich dafür, bei einem Überlauf des  NumberDisplay Objekts der Minuten das NumberDisplay-Objekt der Stunden hochzuzählen. Es gibt keine direkte Verbindung der beiden NumberDisplay-Objekte. Es ist günstiger für die Wartbarkeit und Wiederverwendbarkeit, dass die NumberDisplay-Klasse diese Aufgabe übernimmt.

  1.Verändern Sie das Design so, dass ein NumberDisplay Objekt einem zweiten, übergeordneten NumberDisplay Objekt den Überlauf direkt in seiner
  increment Methode weitergibt. Legen Sie dafür zunächst eine Exemplarvariable parent vom Typ NumberDisplay an (Änderung in der Klasse 
  NumberDisplay). Passen Sie danach die increment Methode an, dass auf parent zugegriffen wird. Da nicht jedes NumberDisplay ein übergeordneten
  parent hat, werden Sie für diese Aufgabe das Schlüsselwort null verwenden müssen. Recherchieren Sie dies im Internet.
    
  2.Fügen Sie einen Konstruktor in der Klasse NumberDisplay hinzu, der zusätzlich zu dem rollOverLimit als zweiten Parameter das übergeordnete
  NumberDisplay Objekt übergibt und es in der parent Variablen speichert.
  
  3.Ändern Sie die Erzeugung des minutes Objekts in ClockDisplay so, dass Sie das hours Objekt übergeben.
  
```java
  public class ClockDisplay {
    private NumberDisplay hours;
    private NumberDisplay minutes;
    private String displayString;    
    
    public ClockDisplay(){
        hours = new NumberDisplay(24, null);
        minutes = new NumberDisplay(60, hours);
        updateDisplay();
    }
    public ClockDisplay(int hour, int minute){
        hours = new NumberDisplay(24, null);
        minutes = new NumberDisplay(60, hours);
        setTime(hour, minute);
    }
    public void timeTick(){
        minutes.increment();
        updateDisplay();
    }
    public void setTime(int hour, int minute) {
        hours.setValue(hour);
        minutes.setValue(minute);
        updateDisplay();
    }

    public String getTime() {
        return displayString;
    }
    
    private void updateDisplay() {
        displayString = hours.getDisplayValue() + ":" + 
                        minutes.getDisplayValue();
    }
}


public class NumberDisplay
{
    private int limit;
    private int value;
    private NumberDisplay parent;
    
    public NumberDisplay(int rollOverLimit, NumberDisplay eltern)    {
        limit = rollOverLimit;
        value = 0;
        parent = eltern;
    }
    
    public NumberDisplay(int rollOverLimit)    {
        limit = rollOverLimit;
        value = 0;
        parent = null;
    }

    public int getValue()    {
        return value;
    }

    public String getDisplayValue()    {
        if(value < 10) {
            return "0" + value;
        }
        else {
            return "" + value;
        }
    }

    public void setValue(int replacementValue)    {
        if((replacementValue >= 0) && (replacementValue < limit)) {
            value = replacementValue;
        }
    }

    public void increment() {
        value = (value + 1) % limit;
        if(value == 0 && parent != null)
        parent.increment();
    }
}
```
