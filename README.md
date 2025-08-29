# Präsentation: Einfach verkettete Liste

---

## 1. Einführung

- **Datenstruktur** = organisierte Sammlung von Daten zur effizienten Verarbeitung  
- Unterschiedliche Typen: Arrays, Listen, Bäume, Stacks, Queues …  
- **Unser Thema:** *Einfach verkettete Liste* (*Singly Linked List*)

---

## 2. Allgemeine Definition

- Eine **einfach verkettete Liste** ist eine **dynamische Datenstruktur**
- Besteht aus **Knoten (Nodes)**
- Jeder Knoten speichert:
  - **Datenwert**
  - **Zeiger (Pointer) auf den nächsten Knoten**
- Das Ende wird durch `NULL` markiert

---

## 3. Einsatzbereiche

Die **einfach verkettete Liste** ist eine Grundlage vieler komplexerer Datenstrukturen und wird in der Praxis häufig genutzt.

### 1. Programmiersprachen
- **Java**: `LinkedList`-Klasse in der Java Collections Library  
- **C++**: `std::forward_list` (speziell für einfach verkettete Listen)  
- **Python**: interne Implementierungen von Queues oder Graphen können verkettete Listen verwenden  

---

### 2. Algorithmen
- **Hash-Tabellen mit Verkettung**:  
  - Bei einer Kollision (zwei Schlüssel haben denselben Hash-Wert) werden die Elemente in einer verketteten Liste gespeichert.  
- **Graphen**:  
  - Adjazenzlisten zur Speicherung von Nachbarknoten.  
- **Stacks und Queues**:  
  - Lassen sich effizient mit einfach verketteten Listen umsetzen.  

---

### 3. Betriebssysteme
- **Speicherverwaltung**:  
  - Freie Speicherblöcke werden oft in einer verketteten Liste organisiert.  
- **Prozessverwaltung**:  
  - Warteschlangen von Prozessen können mit Listen dargestellt werden.  

---

### 4. Datenbanken
- **Indexverwaltung**:  
  - Verkettete Strukturen können für interne Speicherorganisation genutzt werden.  
- **Transaktions-Logs**:  
  - Reihen von Änderungen können als Liste gespeichert werden.  

---

### 5. Alltagsbeispiele (anschaulich)
- **Musik-Playlist** (z. B. Spotify): Titel werden dynamisch hinzugefügt/entfernt  
- **Undo/Redo-Funktion** in Programmen: Schritte werden in einer Liste gespeichert  
- **Browser-Verlauf**: Vor- und Zurück-Navigation basiert auf verketteten Strukturen  

---

## 4. Aufbau und Funktionsweise

### 4.1 Grafische Darstellung

```
  Head
   |
   v
+------+-------+      +------+-------+      +------+-------+
| Data | Next  | ---> | Data | Next  | ---> | Data | Next  | ---> NULL
+------+-------+      +------+-------+      +------+-------+
```

#### Legende

- **Head:** Start des Listenobjekts (Zeiger auf das erste Element)
- **Data:** Datenfeld des Listenobjekts (enthält die gespeicherten Informationen)
- **Next:** Zeiger auf das nächste Listenobjekt (Verbindung zum nächsten Element)
- **NULL:** Ende der Liste (kein weiteres Element vorhanden)

---

### 4.2 Strukturierte Darstellung

| Listenobjekt | Data       | Next         |
|--------------|------------|--------------|
| Head         | Wert 1     | Zeiger auf 2 |
| Objekt 2     | Wert 2     | Zeiger auf 3 |
| Objekt 3     | Wert 3     | NULL         |

- Die Liste besteht aus einzelnen **Objekten (Nodes)**.
- Jeder Node enthält:
  - **Data**: den Wert/die Information
  - **Next**: Verweis auf das nächste Element
- Das letzte Element zeigt mit **Next** auf **NULL** → Ende der Liste.

---

### 4.3 Visualisierung

```plaintext
Head
 |
 v
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  Data: A    │ -> │  Data: B    │ -> │  Data: C    │ -> NULL
│  Next: o----┘    │  Next: o----┘    │  Next: NULL │
└─────────────┘    └─────────────┘    └─────────────┘
```

---

### 4.4 Eigenschaften

- Der **Head** zeigt auf den ersten Knoten  
- Jeder Knoten zeigt auf seinen Nachfolger  
- Zugriff nur durch **Traversieren** der Liste  

---

## 5. Wichtige Operationen

### 5.1 Einfügen (Insert)

- **Am Anfang:** Neuer Knoten wird Head
- **Am Ende:** Neuer Knoten zeigt auf `NULL`
- **In der Mitte:** Verknüpfungen der Zeiger werden angepasst

**Skizze:**

Vorher:  
`A → B → C`

Insert(X nach A):  
`A → X → B → C`

---

### 5.2 Löschen (Delete)

- Gesuchter Knoten wird „übersprungen“

**Skizze:**

Vorher:  
`A → B → C`

Delete(B):  
`A → C`

---

### 5.3 Suchen (Search)

- Vom Head aus alle Elemente durchlaufen
- Laufzeit: **O(n)**

---

### 5.4 Traversieren

- Vom Head starten
- Jeden Knoten der Reihe nach besuchen
- Anwendung: Ausgabe der Werte

---

## 6. Vor- und Nachteile

### Vorteile ✅

- Dynamische Speicherverwaltung
- Einfaches Einfügen und Löschen (wenn Position bekannt)
- Speicher kann flexibel wachsen

### Nachteile ❌

- Kein direkter Indexzugriff
- Höherer Speicherbedarf (Zeiger)
- Langsamer beim Suchen als Arrays

---

## 7. Implementierung in C

```c
#include <stdio.h>
#include <stdlib.h>

// Definition eines Knotens
struct Node {
    int data;
    struct Node* next;
};

// Neuen Knoten am Anfang einfügen
void insertFront(struct Node** head, int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = *head;
    *head = newNode;
}

// Knoten mit bestimmtem Wert löschen
void deleteNode(struct Node** head, int value) {
    struct Node* temp = *head;
    struct Node* prev = NULL;

    while (temp != NULL && temp->data != value) {
        prev = temp;
        temp = temp->next;
    }
    if (temp == NULL) return; // nicht gefunden

    if (prev == NULL) {
        *head = temp->next; // erster Knoten
    } else {
        prev->next = temp->next; // überspringen
    }
    free(temp);
}

// Liste durchlaufen und ausgeben
void printList(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

// Beispielnutzung
int main() {
    struct Node* head = NULL;

    insertFront(&head, 10);
    insertFront(&head, 20);
    insertFront(&head, 30);

    printf("Liste: ");
    printList(head);

    deleteNode(&head, 20);
    printf("Nach Delete: ");
    printList(head);

    return 0;
}
```

---

## 8. Fazit

- Einfach verkettete Liste = Grundlage vieler komplexerer Strukturen
- Gut für dynamische Datenmengen
- Nicht optimal für schnellen Zugriff per Index
- Wichtige Basistechnik für Informatik & Programmierung

---
