#  Präsentation: Einfach verkettete Liste

# Präsentation: Einfach verkettete Liste

## 1. Einführung

- **Datenstruktur** = organisierte Sammlung von Daten zur effizienten Verarbeitung  
- Unterschiedliche Datenstrukturen: Arrays, Listen, Bäume, Stacks, Queues …  
- **Unser Thema:** *Einfach verkettete Liste* (Singly Linked List)  

---

## 3. Aufbau und Funktionsweise

### Grafische Darstellung

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

### Strukturierte Darstellung

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

### Visualisierung

```plaintext
Head
 |
 v
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  Data: A    │ -> │  Data: B    │ -> │  Data: C    │ -> NULL
│  Next: o----┘    │  Next: o----┘    │  Next: NULL │
└─────────────┘    └─────────────┘    └─────────────┘
```

- **Vorteile:** Flexible Größe, einfaches Einfügen/Löschen von Elementen
- **Nachteile:** Kein direkter Zugriff auf ein Element (wie bei Arrays), zusätzlicher Speicher für Zeiger
