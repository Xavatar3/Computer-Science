## Boolean Thinking
Boolean logic reduces everything to two states:
- **1** → true → high → on  
- **0** → false → low → off  

There is no “maybe” or fractions.

### Core Operations

**NOT (¬A)**  
- Inversion: if A is true, ¬A is false; if A is false, ¬A is true.  
- Think: a light switch flipped.

**AND (A · B)**  
- Both must be true; one false input makes the output false.  
- Example: Two ingredients required to bake a cake (A = flour, B = eggs): `A · B`

**OR (A + B)**  
- At least one must be true; only false when all inputs are false.  
- Example: You can watch a movie if it’s Friday **or** you have free time: `Friday + FreeTime`

**Important:** `+` and `·` are logical, not arithmetic.  
`1 + 1 = 1` is perfectly valid here.

### Reading Boolean Expressions

Expression:  
`A · ¬B + C`

Read as:  
> “A AND NOT B, OR C”

Order of operations:  
1. NOT  
2. AND  
3. OR

### Translating Reality into Logic

Example:  
> “The light turns on if the switch is up AND the bulb is functional.”

Let:  
- S = switch up  
- B = bulb functional  

Logic expression:  
`S · B`

---