# SKILL_PCELL
Development of PCELLS using SKILL.

## What is a PCELL?
A PCELL or parameterized cell is a programmable design entity that allows us to create different custom instances each time we place it in a design window.

### Advantages:
- Speed up the layout entry process by eliminating the need to create duplicate versions of the same functional part.
- Save disk space by creating a library of cells for similar parts that are all linked to the same source.
- Eliminate the errors that can result in maintaining multiple versions of the same cell.
- Eliminate the need to explode levels of hierarchy when we want to change a small detail of a design.

## What makes up a SKILL PCELL?
- PCELLS are SKILL programs. It can be composed of the main procedure and often sub-procedures.
- The compilation of the SKILL program creates a new cellview.
- The subprocesses used must be stored and made available when the library is used. It is generally stored in the `.libinit` file, and automatically loaded through the `.libinit` mechanism when the library is opened.

## Using Relative Object Design (ROD) Commands to create design data

### ROD
Relative objective design is a set of high-level SKILL functions for defining simple or complex layout objects and persistent spatial relationships between them.

ROD is useful in
- Creating simple shapes such as rectangles.
- Creating complex shapes such as guard-rings, transistors.
- Associate a signal with a shape.
- Align ROD objects with each other or with fixed coordinates.
- Assign a name to a shape.
- Access points and other information are stored on ROD objects through all levels of hierarchy.
- Create PCELLS using the ROD construct.
