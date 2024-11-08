Here’s a list of some key Elasticsearch query types and operators, with detailed explanations and examples.

### 1. **match**
   - Finds documents that match a provided text, analyzing it according to the field’s analyzer.
   - **Example**:
     ```json
     {
       "query": {
         "match": {
           "description": "Elasticsearch tutorial"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where the `description` field contains terms similar to "Elasticsearch tutorial."

### 2. **term**
   - Finds documents that contain the exact term specified in a field. Useful for keyword (non-analyzed) fields.
   - **Example**:
     ```json
     {
       "query": {
         "term": {
           "status": "active"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where the `status` field exactly matches "active."

### 3. **terms**
   - Finds documents where the field matches any of the given terms (like an OR operator).
   - **Example**:
     ```json
     {
       "query": {
         "terms": {
           "status": ["active", "pending"]
         }
       }
     }
     ```
   - **Explanation**: Matches documents where the `status` is either "active" or "pending."

### 4. **bool**
   - Combines multiple queries using `must`, `must_not`, `should`, and `filter`.
   - **Example**:
     ```json
     {
       "query": {
         "bool": {
           "must": [
             { "term": { "status": "active" } }
           ],
           "must_not": [
             { "term": { "category": "spam" } }
           ],
           "should": [
             { "term": { "priority": "high" } }
           ]
         }
       }
     }
     ```
   - **Explanation**:
     - `must`: Documents must match this condition (`status` is "active").
     - `must_not`: Documents must not match this condition (`category` is "spam").
     - `should`: Documents matching this condition (`priority` is "high") are scored higher.

### 5. **must**
   - Specifies that the query inside `must` must be satisfied.
   - **Example**:
     ```json
     {
       "query": {
         "bool": {
           "must": [
             { "term": { "status": "active" } }
           ]
         }
       }
     }
     ```
   - **Explanation**: Only documents with `status` as "active" will be returned.

### 6. **must_not**
   - Specifies that the query inside `must_not` must not be satisfied.
   - **Example**:
     ```json
     {
       "query": {
         "bool": {
           "must_not": [
             { "term": { "category": "spam" } }
           ]
         }
       }
     }
     ```
   - **Explanation**: Only documents where `category` is not "spam" will be returned.

### 7. **should**
   - Specifies optional conditions. Documents that match these conditions get a higher relevance score.
   - **Example**:
     ```json
     {
       "query": {
         "bool": {
           "should": [
             { "term": { "priority": "high" } },
             { "term": { "priority": "medium" } }
           ]
         }
       }
     }
     ```
   - **Explanation**: Documents with `priority` as "high" or "medium" are given a higher score but aren't required.

### 8. **filter**
   - Similar to `must`, but does not affect the score of the query, making it more efficient for caching.
   - **Example**:
     ```json
     {
       "query": {
         "bool": {
           "filter": [
             { "term": { "status": "active" } }
           ]
         }
       }
     }
     ```
   - **Explanation**: Filters documents where `status` is "active" without affecting the relevance score.

### 9. **wildcard**
   - Matches documents with terms matching a specified pattern, using `*` for multiple characters and `?` for a single character.
   - **Example**:
     ```json
     {
       "query": {
         "wildcard": {
           "username": "jo*"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where `username` starts with "jo" (e.g., "john", "joshua").

### 10. **range**
   - Finds documents with values within a specific range. Useful for numeric or date fields.
   - **Example**:
     ```json
     {
       "query": {
         "range": {
           "age": {
             "gte": 30,
             "lte": 40
           }
         }
       }
     }
     ```
   - **Explanation**: Matches documents where `age` is between 30 and 40, inclusive.

### 11. **exists**
   - Finds documents where a particular field exists or is missing.
   - **Example**:
     ```json
     {
       "query": {
         "exists": {
           "field": "email"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where the `email` field is present.

### 12. **prefix**
   - Matches terms that start with a specified prefix.
   - **Example**:
     ```json
     {
       "query": {
         "prefix": {
           "product_name": "elast"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where `product_name` starts with "elast" (e.g., "elasticsearch").

### 13. **fuzzy**
   - Finds terms that are similar to the given term based on a specified edit distance.
   - **Example**:
     ```json
     {
       "query": {
         "fuzzy": {
           "name": {
             "value": "john",
             "fuzziness": "AUTO"
           }
         }
       }
     }
     ```
   - **Explanation**: Matches documents where `name` is close to "john" (e.g., "john", "jhon").

### 14. **regexp**
   - Matches documents based on a regular expression pattern.
   - **Example**:
     ```json
     {
       "query": {
         "regexp": {
           "username": "jo.*"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where `username` starts with "jo" and can have any characters afterward.

### 15. **match_phrase**
   - Finds documents that contain an exact phrase within a field.
   - **Example**:
     ```json
     {
       "query": {
         "match_phrase": {
           "description": "quick brown fox"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where `description` contains the exact phrase "quick brown fox."

### 16. **match_all**
   - Returns all documents in the index, typically used when you need all documents without filtering.
   - **Example**:
     ```json
     {
       "query": {
         "match_all": {}
       }
     }
     ```
   - **Explanation**: Matches all documents in the index.

### 17. **script**
   - Uses custom scripts to filter documents based on complex conditions.
   - **Example**:
     ```json
     {
       "query": {
         "script": {
           "script": "doc['age'].value > 25"
         }
       }
     }
     ```
   - **Explanation**: Matches documents where the `age` field is greater than 25.
