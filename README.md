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

ROD simplifies the creation of layout entities in SKILL by providing these facilities:
- An object can be accessed in a hierarchy by its name.
- Points on an object can be referenced by name (ll, ur).
- Alignment of ROD objects is fast and effective.
- Complex structures involving several layers can be created easily. 
- Technology information can be used so that ROD structures are process-independent.

### 3.3 ROD Concepts

- *Named objects*

ROD allows for an assignment of a name to any shape. Any instance already has a name, and ROD allows us to reference an instance by its name.
- *Object handles*

A handle is an item of information about a ROD object, such as a point on the object's bounding box. There are two kinds of ROD handles:
- 1. System Defined
  -  Automatically defined when a ROD object is created. Calculated on-demand as they are accessed. 
- 2. User-Defined
  - User-created to store calculations, special coordinates, or other data. Stored in memory and saved to the database.
 
- *Object alignment*

We can align ROD objects with respect to each other. Once established, the alignment is enforced when either object is moved.

- *Connectivity assignment*

For a ROD shape, we can specify connectivity by associating the shape with a specific terminal and net. We can make the shape into a pin.

- *Multipart paths*

A multipart path is a ROD object composed of multiple shapes. A multipart path consists of a single master path and one or more subparts (offset subpath, enclosure subpath, set of sub-rectangles). Generally, complex structures like Buses, Guard-rings, Contact arrays, Transistors are defined with multipart paths.  

- *ROD object structure*

A ROB Object contains:
- 1. Hierarchical name
- 2. Cellview ID
- 3. Database ID
- 4. Transformation information (rotation, mag, and offset)
- 5. Alignment information
- 6. Number of segments 
- 7. Names of user-defined handles
- 8. Names of system-defined handles

### 3.4 Converting Database objects to ROD Objects

We can convert an existing database object to a ROD object using the `rodNameShape` command.
```
rodNameShape(
  [?name S_name]
  ?shapeId d_shapeId
  [?permitRename g_permitRename]) 
```

### 3.5 ROD Functions

#### 3.5.1 Object creation
1. rodCreatePath

2. rodCreatePolygon

3. rodCreateRect

rodAddMPPChopHole
#### 3.5.2 Object alignment
rodAlign rodUnalign
#### 3.5.3 Object information
1. rodGetObj rodlsObj

2. rodNameShape rodUnNameShape rodGetNamedShapes

3. rodGetHandle rodlsHandle

4. rodCreateHandle rodDeleteHandle rodAssignHandleToParameter

5. rodCheck rodlsFigNameUnused

##### 3.5.1.1 rodCreateRect
This function creates a single rectangle, an array of rectangles or fills a bounding box with rectangles.

```
rodCreateRect(
  [?name t_name]
  ?layer txl_layer
  [?width n_width]
  [?length n_length]
  [?origin l_origin]
  [?bBox l_bBox]
  [?elementsX x_elementsX]
  [?elementsY x_elementsY]
  [?spaceX n_spaceX]
  [?spaceY n_spaceY]
  [?cvId d_cvId]
  [?fillBBox l_fillBBox]
  [?size txf_size]
  [?subRectArray l_subrectArgs]
 )
 
 ```
 [*Examples*]
 
 1. Create a single rectangle with a bBox:
 ```
 rodCreateRect(
  ?cvId geGetEditCellView()
  ?layer "m1"
  ?bBox list(2:3 5:7)
 )
 ```
 2. Create a rectangle named "myRx" using width and length arguments:
 ```
 rodCreateRect(
  ?cvId geGetEditCellView()
  ?layer "m3"
  ?length 3
  ?width 4
  ?name "myRx"
)
```
3. Create a 3-by-4 array of unit squares starting at th origin. Separate them by 2 units horizontally and 1 unit vertically:
```
rodCreateRect(
  ?cvid geGetEditCellView()
  ?layer list("m1" "pin")
  ?width 1
  ?length 1
  ?elementsX 3
  ?elementsY 4
  ?spaceX 2
  ?spaceY 1
)
```


- 1. Get the cellview and assign it to a variable called cv.
```
procedure( SrGetRectCV()
  cv = dbFindOpenCellView(ddGetObj("lib") "cellname" "viewname")
  )
 
```
- 2. Create a rectangle and place it into the layout cellview.
```
procedure( SrGate()
  rodCreateRect(
    ?cvId cv
    ?name "gate"
    ?layer "poly"
    ?width 0.6
    ?length 3.6
  )
)
```
- 3. Create two pins "upperPin" and "lowerPin".
```
procedure( SrPins()
  rodCreateRect(
    ?cvId cv
    ?name "upperPin"
    ?layer list("poly" "pin")
    ?width 0.6
    ?length 0.3
    ?origin 1:4
    ?pin t
    ?termName "G"
  )
  
   rodCreateRect(
    ?cvId cv
    ?name "lowerPin"
    ?layer list("poly" "pin")
    ?width 0.6
    ?length 0.3
    ?origin 2:0
    ?pin t
    ?termName "G"
  ) 
```
- 4. Align the "upperPin" with the "gate"
```
procedure( SrAlignTop()
  rodAlign(
    ?alignObj rodGetObj("upperPin" cv)
    ?alignHandle "upperCenter"
    ?refObj rodGetObj("gate" cv)
    ?refHandle "upperCenter"
  )
)
```
- 5. Align the "lowerPin" with the "gate"
```
procedure( SrAlignLower()
  rodAlign(
    ?alignObj rodGetObj("lowerPin" cv)
    ?alignHandle "lowerCenter"
    ?refObj rodGetObj("gate" cv)
    ?refHandle "lowerCenter"
  )
)
```
- 6. Create another gate similar to the one created using multipart path.
```
procedure( SrAnotherGate()
  rodCreatePath(
    ?cvId cv
    ?name "gate2"
    ?layer "poly"
    ?width 0.6
    ?pts list(3:1 3:4.6)
    ?subRect list(
      list(
        ?layer list("poly" "pin")
        ?pin t
        ?termName "G"
        ?width 0.6
        ?length 0.3
        ?space 3.0
      )
    )
  )
)
```
- 6. Align both the gates
```
procedure( SrAlignBoth()
  rodAlign(
    ?alignObj rodGetObj("gate2" cv)
    ?alignHandle "centreLeft"
    ?refObj rodGetObj("gate" cv)
    ?refHandle "centreRight"
    ?xSep 1.0
  )
)

```
 
