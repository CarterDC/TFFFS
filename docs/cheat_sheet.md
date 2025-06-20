# Markdown Cheatsheet
I haven't used markdown in quite some time,
And now I have MkDocs / MkDocs-Material.

Let's see what we can do with these new toys.

## 1. Headings

### Syntax:
* ```# Heading 1```    
* ```## Heading 2```  
* ```### Heading 3```

### Output:
*note : output of a level 1 heading at this point would f. up the table of content*
 

---

## 2. Line Break

### Syntax:
* Using two spaces before return to force ```  ``` a new line.  
* Using explicit ```<br>``` tag to force a new line.  

### Output:
* Using two spaces before return to force  
  a new line.  
* Using explicit ```<br>``` tag to force <br> a new line.  

---

## 3. Bold & Italic Text

### Syntax:
* ```**Bold text**```  
* ```*Italic text*```  
* ```***Bold and Italic***```
### Output:
* **Bold text**  
* *Italic text*  
* ***Bold and Italic***  

---

## 4. Lists 

### Unordered Lists
#### Syntax:

- ```- Item 1``` (bullet can be either ```-```, ```+``` or ```*```)
- ```+ Item 2```
- ```....* Nested Item``` (indent = space x4)

#### Output:
- Item 1
+ Item 2
    * Nested Item

### Ordered Lists
#### Syntax:
- ```1. First Item```
- ```2. Second Item```
- ```....1. First nested Item``` (indent = space x4) 
- ```....2. Second nested Item```

#### Output:
1. First item
2. Second item
    1. First nested Item (auto-numbering corrected to ```a, b, ...```)
    2. Second nested Item

---

## 5. Links

### Syntax:
- ```[Displayed Text](Actual link)```
- ```[Visit Google](https://www.google.com)```
- ```[Visit other file](otherFile.md)```
- ```[Visit other section](myFile.md#other-section)```

### Output:
- [Visit Google](https://www.google.com)
- [Return to Index](index.md)
- [Visit 'Line Break' section](cheat_sheet.md#2-line-break)

---

## 6. Images 

### Syntax:
- ```![Alt text](Image link)```

### Output:
- ![dead link]()
- ![random local lemur](assets/lemur.jpg)

---

## 7. Code Blocks

### Syntax:
- This is ``` ` ```inline code``` ` ``` (back tick : ctrl + alt + 7)
- This is multi-line code block
TODO : use code blocks to write syntax examples
- Lexers : ps1, Bash, [etc...](https://pygments.org/docs/lexers/#pygments.lexers.markup.MarkdownLexer) 
### Output:
- This is `inline code` 
```
This is  
    multi-line  
    code block
```
``` bash title="My Title Here"
print("Hello, World!")
```

---

## 8. Tables

### Syntax:
todo : à refaire
### Output:
| Column 1 | Column 2 |
|-|-|
| Data 1 | Data 2 |

---

## 9. Horizontal Line  

### Syntax:
```---```
### Output:
---

---


## 10. Collapsible Sections 

### Syntax:
``` md title="Markdown"
<details>
  <summary>Click to expand</summary>
  Hidden content here!
</details>
```

### Output:
<details>
  <summary>Click to expand</summary>
  Hidden content here!
</details>
---