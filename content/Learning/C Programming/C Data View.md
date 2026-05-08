---
id: C Data View
aliases: C Programming Language Data View
tags:
  - C
  - dataview
author: S.Sunhaloo
date: 2024-11-05
---

## In Progress

```dataview
TABLE tags, date
FROM "Learning/C Programming"
WHERE status = "In-Progress"
```

## On Hold

```dataview
TABLE tags, date
FROM "Learning/C Programming"
WHERE status = "HOLD"
```

# C Folder

```dataview
TABLE tags, date
FROM "Learning/C Programming"
WHERE file.name != "C Data View"
SORT file.name ASC
```

## C Basics Folder

```dataview
TABLE tags, status, date
FROM "Learning/C Programming/C Basics"
WHERE file.name != "C Data View"
SORT date ASC
```

## Random C Codes Folder

```dataview
TABLE tags, status, date
FROM "Learning/C Programming/Random C Codes"
WHERE file.name != "C Data View"
SORT date ASC
```

---

# Linking C Files

## C Basics Folder

- [[C Language Basics]]
- [[C - Pointers and Function Pointers]]

### C Data Structures Folder

- [[REDO C - Static Arrays]]
- [[C - Structs]]

### C Systems Programming

- [[C - POSIX Compliant Threads Temp]]
- [[C - Process Management and Forks Temp]]

## Random C Codes Folder

### Notes Related

- [[C - Using Multiple Files]]

### For Fun

- [[C - Type Function from Python]]
- [[C - Progress Bar ( Python )]]
- [[C - Grids and Pyramids]]