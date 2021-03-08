# Match Algorithmus

Der Matching Prozess von VOTO basiert auf einem relativ simplen aber effiziente Algorithmus.

Grundlegend wird die Zustimmung eines Statements mit 5 verschiedenen Stufen prozentual bewertet. Der Nutzer kann auswählen:

| Slider Text         | Gespeicherter Wert |
| ------------------- | ------------------ |
| Stimme voll zu      | 100                |
| Stimme eher zu      | 75                 |
| Neutral             | 50                 |
| Stimme weniger zu   | 25                 |
| Stimme gar nicht zu | 0                  |

Je nachdem ob der Nutzer sich dafür entscheidet eine These als wichtig einzustufen wird der Wert doppelt gewichtet.

Die Beantwortung der Thesen wird in einem Array gespeichert und nach der letzten Abstimmung an eine Functio geschickt die die Matches berechnet:

### Schritt 1: Kandidierende laden

Für die angegebene Wahl werden alle Kandidierende, die VOTO bereits ausgefüllt haben aus der Datenbank geladen.

### Schritt 2: Neutrale Thesen überspringen

Es werden alle Thesen des Nutzers, die neutral beantwortet wurden nicht gezählt und nicht in die Berechnung mit eingezogen. Der Rest wird weiter verarbeitet.

### Schritt 3: Berechnung der Punktzahl

Durch die dynamische Anzahl an Thesen sowie das Überspringen von neutralen Abstimmungen variiert die maximale Punktzahl, die bei einem Match erreicht werden kann.

Die maximale Punktzahl (am Anfang 0) ergibt sich aus der Summe der Formel, die bei jeder These aufgerufen wird:

```typescript
maxPoints += = 2.0 * userWeight * candidateWeight;
```

Die tatsächlich erreichten Punkte für eine These wird nun wie folgt berrechnet:

```typescript
const addPoints =
  ((4 - Math.abs(userVote - candidateVote) / 25) / 2) *
  userWeight *
  candidateWeight;
points += addPoints;
```

### Schritt 4: Verarbeiten der Gesamtpunktzahl

Nachdem die Punktzahl aller Thesen wie oben beschrieben für jeden Kandidierenden berechnet und addiert wurde, wird das Resultat gerundet und in Prozent zurückgegeben:

```typescript
return Math.round((points / maxPoints) * 10000) / 100;
```

---

## Fallbeispiel:

Nehmen wir an, wir haben für ein einfaches Beispiel nur 5 Thesen.

Die Beantwortung des Nutzers und des Kandidats lautet:

<table>
 <tr>
  <th >These</th>
  <th colspan="2"> Wähler</th>
  <th colspan="2"> Kandidat A</th>
  <th colspan="2"> Kandidat B</th>
 </tr>
 <tr>
  <td>&nbsp;</td>
  <td>Wert</td>
  <td>Wichtige Frage</td>
  <td>Wert</td>
  <td>Wichtige Frage</td>
  <td>Wert</td>
  <td>Wichtige Frage</td>
 </tr>
 <tr>
 <td>0</td>
  <td>25</td>
 <td>⬜️ </td>
 <td>0</td>
 <td>⬜️ </td>
 <td>25</td>
  <td>✅ </td>
 </tr>
  <tr>
 <td>1</td>
  <td>100</td>
 <td>⬜️ </td>
 <td>75</td>
 <td>✅ </td>
 <td>75</td>
  <td>⬜️ </td>
 </tr>
   <tr>
 <td>2</td>
  <td>75</td>
 <td>✅ </td>
 <td>50</td>
 <td>⬜️ </td>
 <td>100</td>
  <td>⬜️ </td>
 </tr>
    <tr>
 <td>3</td>
  <td>50</td>
 <td>⬜️  </td>
 <td>0</td>
 <td>⬜️ </td>
 <td>0</td>
  <td>⬜️ </td>
 </tr>
  <tr>
 <td>4</td>
  <td>0</td>
 <td>⬜️  </td>
 <td>100</td>
 <td>⬜️ </td>
 <td>50</td>
  <td>⬜️ </td>
 </tr>
</table>

Zuerst werden nun also die Kandiderende geladen, was in unserem Beispiel schon der Fall ist.

Anschließend werden die Thesen aussortiert, die von einem Nutzer als `neutral` eingestuft wurden. Damit ergibt sich folgende Datenstruktur des Nutzers:

```json
{
  "0": {
    "value": 25,
    "weight": 1
  },
  "1": {
    "value": 100,
    "weight": 1
  },
  "2": {
    "value": 75,
    "weight": 2
  },
  "4": {
    "value": 0,
    "weight": 1
  }
}
```

Es folgt die Berechnung der Punktzahl für jede These:

#### Kandidat A:

| These | Maximale Punktzahl | Punktzahl                                                         |
| ----- | ------------------ | ----------------------------------------------------------------- |
| 0     | `(2 * 1 * 1) = 2`  | <code>((4- &#124;(25-0)&#124; / 25) / 2) \* 1 \* 1 = 1.5</code>   |
| 1     | `(2 * 1 * 2) = 4`  | <code>((4- &#124;(100-75)&#124; / 25) / 2) \* 1 \* 2 = 3.0</code> |
| 2     | `(2 * 2 * 1) = 4`  | <code>((4- &#124;(75-50)&#124; / 25) / 2) \* 2 \* 1 = 3.0</code>  |
| 4     | `(2 * 1 * 1) = 2`  | <code>((4- &#124;(0-100)&#124; / 25) / 2) \* 1 \* 1 = 0.0</code>  |

So ergibt sich die maximal erreichbare Punktzahl: **`12`** sowie die tatsächlich erreichte Punktzahl von **`7.5`**.

Der Rückgabewert für diesen Kandidat ergibt sich nun:

```javascript
((7.5 / 12.0) * 100 = 62.5;
```

Gerundet hat man nun ein Ergebnis von **`63%`**.

---

#### Kandidat B:

| These | Maximale Punktzahl | Punktzahl                                                         |
| ----- | ------------------ | ----------------------------------------------------------------- |
| 0     | `(2 * 1 * 2) = 4`  | <code>((4- &#124;(25-25)&#124; / 25) / 2) \* 1 \* 2 = 4.0</code>  |
| 1     | `(2 * 1 * 1) = 2`  | <code>((4- &#124;(100-75)&#124; / 25) / 2) \* 1 \* 1 = 1.5</code> |
| 2     | `(2 * 2 * 1) = 4`  | <code>((4- &#124;(75-100)&#124; / 25) / 2) \* 2 \* 1 = 3.0</code> |
| 4     | `(2 * 1 * 1) = 2`  | <code>((4- &#124;(0-50)&#124; / 25) / 2) \* 1 \* 1 = 1.0</code>   |

So ergibt sich die maximal erreichbare Punktzahl: **`12`** sowie die tatsächlich erreichte Punktzahl von **`9.5`**.

Der Rückgabewert für diesen Kandidat ergibt sich nun:

```javascript
((9.5 / 12.0) * 100 = 79.17;
```

Gerundet hat man nun ein Ergebnis von **`79%`**.

---

Nach der Berechnung aller Kandiderenden, werden die Ergebnisse sortiert und dem Frontend zurückgegeben. Dort können nun die Matches in ihrer Reihenfolge angezeigt werden und Bilder der Kandidierenden geladen werden.
