# SKILL_PCELL
Development of PCELLS using SKILL.

## 1. What is a PCELL?
A PCELL or parameterized cell is a programmable design entity that allows us to create different custom instances each time we place it in a design window.

### 1.1 Advantages:
- Speed up the layout entry process by eliminating the need to create duplicate versions of the same functional part.
- Save disk space by creating a library of cells for similar parts that are all linked to the same source.
- Eliminate the errors that can result in maintaining multiple versions of the same cell.
- Eliminate the need to explode levels of hierarchy when we want to change a small detail of a design.

## 2. What makes up a SKILL PCELL?
- PCELLS are SKILL programs. It can be composed of the main procedure and often sub-procedures.
- The compilation of the SKILL program creates a new cellview.
- The subprocesses used must be stored and made available when the library is used. It is generally stored in the `.libinit` file, and automatically loaded through the `.libinit` mechanism when the library is opened.

## 3. Using Relative Object Design (ROD) Commands to create design data

### 3.1 What is ROD?
Relative objective design is a set of high-level SKILL functions for defining simple or complex layout objects and persistent spatial relationships between them.

ROD is useful in
- Creating simple shapes such as rectangles.
- Creating complex shapes such as guard-rings, transistors.
- Associate a signal with a shape.
- Align ROD objects with each other or with fixed coordinates.
- Assign a name to a shape.
- Access points and other information are stored on ROD objects through all levels of hierarchy.
- Create PCELLS using the ROD construct.

### 3.2 Why ROD?

ROD simplifies creation of layout entities in SKILL by providing these facilities:
- An object can be accessed in a hierarchy by its name.
- Points on an object can be referenced by name (ll,ur).
- Alignment of ROD objects are fast and effective.
- Complex structures involving several layers can be created easily. 
- Techology information can be used so that ROD structures are process independent.

### 3.3 ROD Concepts

- *Named objects*

ROD allows to assign a name to any shape. Any instance already has a name, and ROD allows us to reference an instance by its name.
- *Object handels*

A handle is an item of information about ROD object, such as a point on the object's bounding box. There are two kinds of ROD handels:
- 1. System Defined
  -  Automatically defined when a ROD object is created. Calculated on-demand as they are accessed. 
- 2. User Defined
  - User created to store calculations, special coordinates, or other data. Stored in memory and saved to the database.
 
- *Object alignment*

We can align ROD objects with respect to each other. Once established, the alignment is enforced when either object is moved.

- *Connectivity assignment*

For a ROD shape, we can specify connectivity by associating the shape with a specific terminal and net. We can make the shape into in a pin.

- *Multipart paths*

A multipart path is a ROD object composed of multiple shapes. A multipart path consist of a single master path and one or more subparts (offset subpath, enclosure subpath, set of subrectangles). Genrally complex structures like Buses, Guard-rings, Contact arrays, Transistors are defined with multipart paths.  

- ROD object structure
