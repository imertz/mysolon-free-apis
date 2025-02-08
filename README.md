# MySolon Utilities Free API

[English](#english) | [Ελληνικά](#greek)

## Table of Contents

### English

- [Base URL](#base-url)
- [Rate Limiting](#rate-limiting)
- [Public Endpoints](#public-endpoints)
  - [Get Random Person](#get-random-person)
  - [Get Random Male Person](#get-random-male-person)
  - [Get Random Female Person](#get-random-female-person)
  - [Validate AFM](#validate-afm)
  - [Athens Metro Elevators Status](#athens-metro-elevator-status)
  - [Non-bank contractual Interest Rates](#non-bank-contractual-interest-rates)
- [Error Responses](#error-responses)
- [Usage Examples](#usage-examples)

### Greek

- [Βασικό URL](#βασικό-url)
- [Όριο Αιτημάτων](#όριο-αιτημάτων)
- [Δημόσια Τελικά Σημεία](#δημόσια-τελικά-σημεία)
  - [Λήψη Τυχαίου Προσώπου](#λήψη-τυχαίου-προσώπου)
  - [Λήψη Τυχαίου Άνδρα](#λήψη-τυχαίου-άνδρα)
  - [Λήψη Τυχαίας Γυναίκας](#λήψη-τυχαίας-γυναίκας)
  - [Επικύρωση ΑΦΜ](#επικύρωση-αφμ)
  - [Κατάσταση Ανελκυστήρων Μετρό Αθήνας](#κατάσταση-ανελκυστήρων-μετρό-αθήνας)
  - [Εξωτραπεζικά Επιτόκια](#εξωτραπεζικά-επιτόκια)
- [Απαντήσεις Σφαλμάτων](#απαντήσεις-σφαλμάτων)
- [Παραδείγματα Χρήσης](#παραδείγματα-χρήσης)

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
  "name": "ΠΑΝΑΓΗΣ",
  "surname": "ΑΜΟΥΤΖΟΠΟΥΛΟΣ",
  "father_name": "ΤΖΟΥΛΙΟΣ",
  "mother_name": "ΑΡΟΔΑΜΗ",
  "adt": "Γ-572977",
  "afm": "294558493",
  "birthdate": "02.09.1956",
  "birthplace": "ΔΗΜΟΣ ΑΒΙΑΣ"
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

### Athens Metro Elevator Status

The latest elevator status of the Metro Stations of Athens, as published in the official site of [Stasy](https://stasy.gr/elevators). Updated every 5 minutes.

```http
GET /elevators
```

**Response Example**

```json
{
  "lines": [
    {
      "id": "line118",
      "stations": [
        {
          "name": "Κηφισιά",
          "status": "ok",
          "elevators": {
            "functional": [
              "Οδός Τατοΐου -Υπόγεια Διάβαση",
              "Αποβάθρα - Υπόγεια Διάβαση"
            ],
            "nonFunctional": []
          },
          "connections": null,
          "note": null
        }
      ]
    }
  ],
  "timestamp": "2025-02-08T10:37:10.018Z",
  "totalLines": 3,
  "totalStations": 71
}
```

### Non-bank contractual Interest Rates

Non-bank contractual interest rates as published by the Bank of Greece. Fetched every six hours from the official site of [Bank of Greece](https://www.bankofgreece.gr/en/statistics/financial-markets-and-interest-rates/interest-rates-applicable-on-ligitation)

```http
GET /epitokia
```

**Response Example**

```json
{
  "epitokia": [
    {
      "Αρχική Ημερομηνία": "18/12/2024",
      "Τελική Ημερομηνία": "04/02/2025",
      "Διοικητική Πράξη": "Ν.2842/2000 αρθρ.3, παρ.2",
      "Α' ΦΕΚ": "207/27.9.2000",
      "Δικαιοπρακτικός": "8,40%",
      "Υπερημερίας": "10,40%"
    },
    {
      "Αρχική Ημερομηνία": "05/02/2025",
      "Τελική Ημερομηνία": "-",
      "Διοικητική Πράξη": "Ν.2842/2000 αρθρ.3, παρ.2",
      "Α' ΦΕΚ": "207/27.9.2000",
      "Δικαιοπρακτικός": "8,15%",
      "Υπερημερίας": "10,15%"
    }
  ],
  "last_check": "2025-02-08T09:17:41.085Z"
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

Δωρεάν API διάφορων Ελληνικών εργαλείων.

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
  "name": "ΠΑΝΑΓΗΣ",
  "surname": "ΑΜΟΥΤΖΟΠΟΥΛΟΣ",
  "father_name": "ΤΖΟΥΛΙΟΣ",
  "mother_name": "ΑΡΟΔΑΜΗ",
  "adt": "Γ-572977",
  "afm": "294558493",
  "birthdate": "02.09.1956",
  "birthplace": "ΔΗΜΟΣ ΑΒΙΑΣ"
}
```

### Δημιουργία Τυχαίου Προσώπου (αρσενικού γένους)

Δημιουργία τυχαίου(-ων) προσώπου(-ων) (αρσενικού γένους) με ελληνικά δημογραφικά στοιχεία

```http
GET /persons/random/male
```

**Παράμετροι Ερωτήματος**
| Παράμετρος | Τύπος | Περιγραφή | Προεπιλογή |
|------------|---------|----------------------------------------|------------|
| count | integer | Αριθμός προσώπων (ελάχ: 1, μέγ: 100) | 1 |

### Δημιουργία Τυχαίου Προσώπου (θηλυκού γένους)

Δημιουργία τυχαίου(-ων) προσώπου(-ων) (θηλυκού γένους) με ελληνικά δημογραφικά στοιχεία

```http
GET /persons/random/female
```

**Παράμετροι Ερωτήματος**
| Παράμετρος | Τύπος | Περιγραφή | Προεπιλογή |
|------------|---------|----------------------------------------|------------|
| count | integer | Αριθμός προσώπων (ελάχ: 1, μέγ: 100) | 1 |

### Έλεγχος ΑΦΜ

Αλγοριθμικός Έλεγχος Αριθμού Φορολογικού Μητρώου (ΑΦΜ)

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

### Κατάσταση Ανελκυστήρων Μετρό Αθήνας

Η τελευταία κατάσταση των ανελκυστήρων των σταθμών του Μετρό της Αθήνας, όπως δημοσιεύεται στην επίσημη ιστοσελίδα της [ΣΤΑΣΥ](https://stasy.gr/elevators). Ενημερώνεται κάθε 5 λεπτά.

```http
GET /elevators
```

**Παράδειγμα Απάντησης**

```json
{
  "lines": [
    {
      "id": "line118",
      "stations": [
        {
          "name": "Κηφισιά",
          "status": "ok",
          "elevators": {
            "functional": [
              "Οδός Τατοΐου -Υπόγεια Διάβαση",
              "Αποβάθρα - Υπόγεια Διάβαση"
            ],
            "nonFunctional": []
          },
          "connections": null,
          "note": null
        }
      ]
    }
  ],
  "timestamp": "2025-02-08T10:37:10.018Z",
  "totalLines": 3,
  "totalStations": 71
}
```

### Εξωτραπεζικά Επιτόκια

Εξωτραπεζικά επιτόκια (δικαιοπρακτικά και υπερημερίας) όπως δημοσιεύονται από την Τράπεζα της Ελλάδος. Ενημερώνεται κάθε έξι ώρες από την επίσημη ιστοσελίδα της [Τράπεζας της Ελλάδος](https://www.bankofgreece.gr/statistika/xrhmatopistwtikes-agores/ekswtrapezika-epitokia).

```http
GET /epitokia
```

**Παράδειγμα Απάντησης**

```json
{
  "epitokia": [
    {
      "Αρχική Ημερομηνία": "18/12/2024",
      "Τελική Ημερομηνία": "04/02/2025",
      "Διοικητική Πράξη": "Ν.2842/2000 αρθρ.3, παρ.2",
      "Α' ΦΕΚ": "207/27.9.2000",
      "Δικαιοπρακτικός": "8,40%",
      "Υπερημερίας": "10,40%"
    },
    {
      "Αρχική Ημερομηνία": "05/02/2025",
      "Τελική Ημερομηνία": "-",
      "Διοικητική Πράξη": "Ν.2842/2000 αρθρ.3, παρ.2",
      "Α' ΦΕΚ": "207/27.9.2000",
      "Δικαιοπρακτικός": "8,15%",
      "Υπερημερίας": "10,15%"
    }
  ],
  "last_check": "2025-02-08T09:17:41.085Z"
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
