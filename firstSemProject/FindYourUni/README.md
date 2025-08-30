
# FindYourUni (Java CLI App)

**FindYourUni** is a Java console application that allows students to rank universities based on their **own chosen criteria and custom weights**. The program reads a dataset containing university stats (like academic reputation, H-index, citations, etc.), lets the user select relevant factors, and assigns a weighted score to each university to output a personalized ranking.

---

## Features

- ✅ Supports any number of ranking factors present in the dataset  
- ✅ Lets users choose which factors matter to them  
- ✅ Users assign **custom weights** to each selected factor (e.g., 40% to Citations, 30% to Academic Rep, etc.)  
- ✅ Reads university data from a `.txt` file  
- ✅ Outputs ranked list of top universities to a new text file  
- ✅ Handles data validation, malformed files, and edge cases gracefully  

---

## Sample Ranking Factors Supported

- Academic Reputation  
- Employer Reputation  
- Citations  
- H-Index  
- International Student Diversity  
- *(...and more depending on dataset)*  

---

## How It Works

1. **User specifies how many ranking factors are present** in the dataset.
2. **User provides names for those factors**, in order (e.g., "Academic Reputation", "Citations", etc.)
3. User is then asked:  
   > Which factors do you want to base your decision on?  
   > (Type their serial numbers. Type `done` when finished)
4. For each selected factor, the user enters its **weightage** (in %, should sum to 100).
5. User provides:
   - 📂 Input file (dataset file)
   - 💾 Output file (where results will be saved)
6. The program:
   - Parses the data
   - Extracts stats for selected factors
   - Computes a **weighted score**
   - Sorts and outputs the **top 30 universities** to the output file

---

## Input File Format (Example)
- Each line contains:
  `University Name ; Country ; Stat1 ; Stat2 ; ...`
- Number of stats must match the number of ranking factors defined

---

## Output File Example
Here are the top 30 universities for Computer Science ranked according to your criteria

Rank 1-:
Name: Massachusetts Institute of Technology (MIT)
Country: United States
Overall score: 95.320

Rank 2-:
Name: Stanford University
Country: United States
Overall score: 93.180
---

## Error Handling & Validation

- Invalid or non-existent input files → user-friendly error
- Stats outside 0–100 range are skipped
- If file contains extra stats beyond expected count → warns and exits
- Weightages must add up to 100%
- Repeated factors or invalid serial numbers are rejected during selection

---

## Notes

- CLI-based, no GUI yet  
- Built with Java Standard Edition only  
- Designed to be robust for both valid and malformed input files  
- Can be extended to support filtering by region, budget, etc.
