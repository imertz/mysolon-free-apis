# MySolon Utilities Free API

[English](#english) | [Ελληνικά](#greek)

---

# English

Free Greek utilities API service.

## Base URL

```
https://apis.mysolon.gr
```

## Rate Limiting

- 1000 requests per hour per IP
- When limit is exceeded, the API returns status code `429`

## Public Endpoints

### Get Random Person

Generate random person(s) with Greek demographics

```http
GET /persons/random
```

**Query Parameters**
| Parameter | Type | Description | Default |
|-----------|---------|--------------------------------------|---------|
| count | integer | Number of persons (min: 1, max: 100) | 1 |

**Response Example**

```json
{
  "name": "ΓΕΩΡΓΙΟΣ",
  "surname": "ΠΑΠΑΔΟΠΟΥΛΟΣ",
  "father_name": "ΙΩΑΝΝΗΣ",
  "mother_name": "ΜΑΡΙΑ",
  "adt": "ΑΚ-123456",
  "afm": "123456789",
  "birthdate": "15.06.1980",
  "birthplace": "ΔΗΜΟΣ ΑΘΗΝΑΙΩΝ"
}
```

### Get Random Male Person

Generate random male person(s) with Greek demographics

```http
GET /persons/random/male
```

**Query Parameters**
| Parameter | Type | Description | Default |
|-----------|---------|--------------------------------------|---------|
| count | integer | Number of persons (min: 1, max: 100) | 1 |

### Get Random Female Person

Generate random female person(s) with Greek demographics

```http
GET /persons/random/female
```

**Query Parameters**
| Parameter | Type | Description | Default |
|-----------|---------|--------------------------------------|---------|
| count | integer | Number of persons (min: 1, max: 100) | 1 |

### Validate AFM

Validate a Greek Tax Registration Number (ΑΦΜ)

```http
GET /validate/afm/{afm}
```

**Parameters**
| Parameter | Type | Description |
|-----------|--------|--------------------|
| afm | string | 9-digit AFM number |

**Response Example**

```json
{
  "afm": "123456789",
  "isValid": true
}
```

## Error Responses

The API uses standard HTTP status codes:

- `400` - Bad Request
- `429` - Too Many Requests
- `500` - Internal Server Error

**Error Response Format**

```json
{
  "error": "Error message here"
}
```

## Usage Examples

### JavaScript

```javascript
// Get a random person
const response = await fetch("https://apis.mysolon.gr/persons/random");
const person = await response.json();

// Validate an AFM
const afm = "123456789";
const response = await fetch(`https://apis.mysolon.gr/validate/afm/${afm}`);
const result = await response.json();
```

---

# Greek

Δωρεάν API υπηρεσία ελληνικών εργαλείων.

## Βασικό URL

```
https://apis.mysolon.gr
```

## Όριο Αιτημάτων

- 1000 αιτήματα ανά ώρα ανά IP
- Όταν ξεπεραστεί το όριο, το API επιστρέφει κωδικό κατάστασης `429`

## Δημόσια Τελικά Σημεία

### Λήψη Τυχαίου Προσώπου

Δημιουργία τυχαίου(-ων) προσώπου(-ων) με ελληνικά δημογραφικά στοιχεία

```http
GET /persons/random
```

**Παράμετροι Ερωτήματος**
| Παράμετρος | Τύπος | Περιγραφή | Προεπιλογή |
|------------|---------|----------------------------------------|------------|
| count | integer | Αριθμός προσώπων (ελάχ: 1, μέγ: 100) | 1 |

**Παράδειγμα Απάντησης**

```json
{
  "name": "ΓΕΩΡΓΙΟΣ",
  "surname": "ΠΑΠΑΔΟΠΟΥΛΟΣ",
  "father_name": "ΙΩΑΝΝΗΣ",
  "mother_name": "ΜΑΡΙΑ",
  "adt": "ΑΚ-123456",
  "afm": "123456789",
  "birthdate": "15.06.1980",
  "birthplace": "ΔΗΜΟΣ ΑΘΗΝΑΙΩΝ"
}
```

### Λήψη Τυχαίου Άνδρα

Δημιουργία τυχαίου(-ων) άνδρα(-ών) με ελληνικά δημογραφικά στοιχεία

```http
GET /persons/random/male
```

**Παράμετροι Ερωτήματος**
| Παράμετρος | Τύπος | Περιγραφή | Προεπιλογή |
|------------|---------|----------------------------------------|------------|
| count | integer | Αριθμός προσώπων (ελάχ: 1, μέγ: 100) | 1 |

### Λήψη Τυχαίας Γυναίκας

Δημιουργία τυχαίας(-ων) γυναίκας(-ών) με ελληνικά δημογραφικά στοιχεία

```http
GET /persons/random/female
```

**Παράμετροι Ερωτήματος**
| Παράμετρος | Τύπος | Περιγραφή | Προεπιλογή |
|------------|---------|----------------------------------------|------------|
| count | integer | Αριθμός προσώπων (ελάχ: 1, μέγ: 100) | 1 |

### Επικύρωση ΑΦΜ

Επικύρωση Αριθμού Φορολογικού Μητρώου (ΑΦΜ)

```http
GET /validate/afm/{afm}
```

**Παράμετροι**
| Παράμετρος | Τύπος | Περιγραφή |
|------------|--------|---------------------|
| afm | string | 9ψήφιος αριθμός ΑΦΜ |

**Παράδειγμα Απάντησης**

```json
{
  "afm": "123456789",
  "isValid": true
}
```

## Απαντήσεις Σφαλμάτων

Το API χρησιμοποιεί τυπικούς κωδικούς κατάστασης HTTP:

- `400` - Εσφαλμένο Αίτημα
- `429` - Υπέρβαση Ορίου Αιτημάτων
- `500` - Εσωτερικό Σφάλμα Διακομιστή

**Μορφή Απάντησης Σφάλματος**

```json
{
  "error": "Μήνυμα σφάλματος εδώ"
}
```

## Παραδείγματα Χρήσης

### JavaScript

```javascript
// Λήψη τυχαίου προσώπου
const response = await fetch("https://apis.mysolon.gr/persons/random");
const person = await response.json();

// Επικύρωση ΑΦΜ
const afm = "123456789";
const response = await fetch(`https://apis.mysolon.gr/validate/afm/${afm}`);
const result = await response.json();
```

## Υποστήριξη

Εάν αντιμετωπίζετε προβλήματα ή έχετε ερωτήσεις:

- Ανοίξτε ένα issue στο GitHub
- Επικοινωνία: support@mysolon.gr

## Άδεια Χρήσης

Αυτό το API παρέχεται υπό την άδεια MIT.
