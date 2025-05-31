## 🎨 1. UI Mockup Description

### **Main Screen**

#### 📄 Upload Area

* **Left Panel**: “Original Document” (file upload or paste text)
* **Right Panel**: “Revised Document” (file upload or paste text)

#### ⚙️ Options Panel

* \[✔️] Ignore grammar-only changes
* \[✔️] Highlight semantic changes
* [ ] Show punctuation-only changes
* \[Drop-down] View Mode:

  * Side-by-side
  * Inline
* \[🔄] Compare Button

---

### **Results View**

#### A. **Comparison Display**

* **Side-by-Side or Inline View**

  * Color-coded:

    * 🔴 Red strike-through = Removed text
    * 🟢 Green underline = Added text
    * 🟡 Yellow highlight = Changed text (with same meaning)
    * 🔵 Blue highlight = Changed text (with different meaning)
* **Hover/Tooltip or Click Pop-up**:

  * Shows interpretation:

    > “Stylistic change, meaning preserved”
    > “Semantic change: tone altered”
    > “Punctuation change only”

#### B. **Summary Panel**

* **Total Lines Compared**: 120
* **Lines Changed**: 25

  * Same-meaning rewrites: 10
  * Meaning-altering edits: 12
  * Grammar-only edits: 3
* **Similarity Score**: 91%

#### C. **Export/Actions**

* \[💾 Export as PDF/Word/JSON]
* \[🔗 Share]
* \[📝 Comment or Review]

---

## 📡 2. API Specification

### **Endpoint**: `/compare-documents`

#### Method: `POST`

#### Headers:

```json
{
  "Content-Type": "application/json",
  "Authorization": "Bearer <token>"
}
```

#### Request Body:

```json
{
  "original_text": "<string>",
  "revised_text": "<string>",
  "options": {
    "ignore_grammar_only": true,
    "show_punctuation_changes": false,
    "output_format": "side_by_side"
  }
}
```

#### Response:

```json
{
  "summary": {
    "lines_total": 120,
    "lines_changed": 25,
    "meaning_preserved": 10,
    "meaning_changed": 12,
    "grammar_only": 3,
    "similarity_score": 91
  },
  "changes": [
    {
      "line_number": 14,
      "original": "The manager approved the request.",
      "revised": "The request was approved by the manager.",
      "type": "grammatical_rewrite",
      "meaning_changed": false,
      "note": "Passive voice rewrite, meaning preserved."
    },
    {
      "line_number": 22,
      "original": "The policy must be updated every quarter.",
      "revised": "The policy should be reviewed quarterly.",
      "type": "semantic_change",
      "meaning_changed": true,
      "note": "Changed from a mandatory update to a suggestion."
    }
  ]
}
```

---

## ✍️ 3. Sample Input-Output

### **Input**

```json
{
  "original_text": "The report was submitted yesterday. The manager approved it.",
  "revised_text": "The report got submitted yesterday. It was approved by the manager.",
  "options": {
    "ignore_grammar_only": false
  }
}
```

### **Output**

```json
{
  "summary": {
    "lines_total": 2,
    "lines_changed": 2,
    "meaning_preserved": 2,
    "meaning_changed": 0,
    "grammar_only": 2,
    "similarity_score": 100
  },
  "changes": [
    {
      "line_number": 1,
      "original": "The report was submitted yesterday.",
      "revised": "The report got submitted yesterday.",
      "type": "grammatical_rewrite",
      "meaning_changed": false,
      "note": "Informal grammatical change."
    },
    {
      "line_number": 2,
      "original": "The manager approved it.",
      "revised": "It was approved by the manager.",
      "type": "passive_voice_change",
      "meaning_changed": false,
      "note": "Passive voice transformation, same meaning."
    }
  ]
}
```

---
