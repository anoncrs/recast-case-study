# Recast eval set

Broken LLM output, then what a correct engine must do.

## 1. Single quotes
Input: {'id': 1, 'ok': true}
Must become valid JSON with double quotes.
Must not drop id or ok.

## 2. Python words
Input: {"ok": True, "name": None}
Must turn True into true and None into null.

## 3. Trailing comma
Input: {"a": 1, "b": 2,}
Must remove the last comma. Must not add a new key.

## 4. Markdown fence
Input: a short sentence, then a fenced json block with {"x": 1}
Must keep only {"x": 1}. Must not keep the sentence.

## 5. Cut-off JSON
Input: {"user": "ana", "items": [1, 2
Must refuse or mark invalid. Must not invent the missing ending.

## 6. JSON inside a sentence
Input: Sure. The payload is {"order": 9, "paid": false} hope that helps!
Must keep only the JSON object.

## 7. Mixed junk
Input: {'total': 15000, 'paid': True,}
Must become {"total": 15000, "paid": true}. Must not change 15000.

## 8. Bad email under a schema
Input: {"email": "not-an-email"}
Must report invalid. Must not invent user@example.com.
