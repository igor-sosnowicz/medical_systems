### Specyfikacja API

#### 1. Autoryzacja

- **Endpoint**: `/api/auth/register`
- **Metoda**: `POST`
- **Opis**: Rejestracja nowego użytkownika.
- **Parametry**:
  - `username` (string, wymagany): Nazwa użytkownika.
  - `password` (string, wymagany): Hasło użytkownika.
  - `email` (string, wymagany): Adres e-mail użytkownika.
- **Odpowiedź**:
  - `201 Created`: 
    ```json
    {
      "message": "User registered successfully."
    }
    ```
  - `400 Bad Request`: 
    ```json
    {
      "error": "Invalid input data."
    }
    ```

- **Endpoint**: `/api/auth/login`
- **Metoda**: `POST`
- **Opis**: Logowanie użytkownika.
- **Parametry**:
  - `username` (string, wymagany): Nazwa użytkownika.
  - `password` (string, wymagany): Hasło użytkownika.
- **Odpowiedź**:
  - `200 OK`: 
    ```json
    {
      "token": "your_auth_token"
    }
    ```
  - `401 Unauthorized`: 
    ```json
    {
      "error": "Invalid credentials."
    }
    ```

#### 2. Zbieranie danych

- **Endpoint**: `/api/data/collect`
- **Metoda**: `POST`
- **Opis**: Zbieranie danych o zachorowaniach.
- **Parametry**:
  - `source` (string, wymagany): Źródło danych (np. "public_health", "social_media").
  - `data` (object, wymagany): Obiekt zawierający dane do zebrania.
    - `date` (string, wymagany): Data zgłoszenia (format: YYYY-MM-DD).
    - `location` (string, wymagany): Lokalizacja zgłoszenia.
    - `cases` (integer, wymagany): Liczba zgłoszonych przypadków.
- **Odpowiedź**:
  - `201 Created`: 
    ```json
    {
      "message": "Data collected successfully."
    }
    ```
  - `400 Bad Request`: 
    ```json
    {
      "error": "Invalid input data."
    }
    ```

#### 3. Analiza danych

- **Endpoint**: `/api/data/analyze`
- **Metoda**: `POST`
- **Opis**: Analiza zebranych danych w celu przewidywania zachorowań.
- **Parametry**:
  - `analysisParameters` (object, wymagany): Parametry analizy.
    - `startDate` (string, wymagany): Data początkowa analizy (format: YYYY-MM-DD).
    - `endDate` (string, wymagany): Data końcowa analizy (format: YYYY-MM-DD).
    - `location` (string, opcjonalny): Lokalizacja do analizy.
- **Odpowiedź**:
  - `200 OK`: 
    ```json
    {
      "predictions": [
        {
          "date": "YYYY-MM-DD",
          "predictedCases": 100
        },
        ...
      ]
    }
    ```
  - `400 Bad Request`: 
    ```json
    {
      "error": "Invalid input data."
    }
    ```

#### 4. Wizualizacja danych

- **Endpoint**: `/api/data/visualization`
- **Metoda**: `GET`
- **Opis**: Pobieranie danych do wizualizacji.
- **Parametry**:
  - `type` (string, wymagany): Typ wizualizacji (np. "map", "chart").
  - `timeframe` (string, opcjonalny): Okres czasu do wizualizacji.
- **Odpowiedź**:
  - `200 OK`: 
    ```json
    {
      "visualizationData": {
        "type": "chart",
        "data": [
          {
            "date": "YYYY-MM-DD",
            "cases": 50
          },
          ...
        ]
      }
    }
    ```
  - `404 Not Found`: 
    ```json
    {
      "error": "No data available for visualization."
    }
    ```

#### 5. Powiadomienia i alerty

- **Endpoint**: `/api/alerts`
- **Metoda**: `GET`
- **Opis**: Pobieranie aktywnych powiadomie
- **Endpoint**: `/api/alerts`
- **Metoda**: `GET`
- **Opis**: Pobieranie aktywnych powiadomień i alertów.
- **Odpowiedź**:
  - `200 OK`: 
    ```json
    {
      "alerts": [
        {
          "id": 1,
          "message": "Alert message 1",
          "recipient": "user@example.com",
          "threshold": 100,
          "createdAt": "YYYY-MM-DDTHH:MM:SSZ"
        },
        {
          "id": 2,
          "message": "Alert message 2",
          "recipient": "user@example.com",
          "threshold": 200,
          "createdAt": "YYYY-MM-DDTHH:MM:SSZ"
        }
      ]
    }
    ```
  - `204 No Content`: 
    ```json
    {
      "message": "No active alerts."
    }
    ```

- **Endpoint**: `/api/alerts`
- **Metoda**: `POST`
- **Opis**: Tworzenie nowego powiadomienia.
- **Parametry**:
  - `message` (string, wymagany): Treść powiadomienia.
  - `recipient` (string, wymagany): Adres e-mail lub numer telefonu odbiorcy.
  - `threshold` (integer, wymagany): Próg alarmowy.
- **Odpowiedź**:
  - `201 Created`: 
    ```json
    {
      "message": "Alert created successfully.",
      "alertId": 1
    }
    ```
  - `400 Bad Request`: 
    ```json
    {
      "error": "Invalid input data."
    }
    ```

- **Endpoint**: `/api/alerts/{id}`
- **Metoda**: `PUT`
- **Opis**: Aktualizacja istniejącego powiadomienia.
- **Parametry**:
  - `id` (integer, wymagany): ID powiadomienia do zaktualizowania.
  - `message` (string, opcjonalny): Nowa treść powiadomienia.
  - `recipient` (string, opcjonalny): Nowy adres e-mail lub numer telefonu odbiorcy.
  - `threshold` (integer, opcjonalny): Nowy próg alarmowy.
- **Odpowiedź**:
  - `200 OK`: 
    ```json
    {
      "message": "Alert updated successfully."
    }
    ```
  - `404 Not Found`: 
    ```json
    {
      "error": "Alert not found."
    }
    ```

- **Endpoint**: `/api/alerts/{id}`
- **Metoda**: `DELETE`
- **Opis**: Usuwanie istniejącego powiadomienia.
- **Parametry**:
  - `id` (integer, wymagany): ID powiadomienia do usunięcia.
- **Odpowiedź**:
  - `204 No Content`: 
    ```json
    {
      "message": "Alert deleted successfully."
    }
    ```
  - `404 Not Found`: 
    ```json
    {
      "error": "Alert not found."
    }
    ```

#### 6. Raportowanie

- **Endpoint**: `/api/reports`
- **Metoda**: `GET`
- **Opis**: Generowanie raportów dotyczących przewidywanych zachorowań.
- **Parametry**:
  - `type` (string, wymagany): Typ raportu (np. "summary", "detailed").
  - `timeframe` (string, opcjonalny): Okres czasu do raportu.
- **Odpowiedź**:
  - `200 OK`: 
    ```json
    {
      "report": {
        "type": "summary",
        "data": [
          {
            "date": "YYYY-MM-DD",
            "predictedCases": 150
          },
          ...
        ]
      }
    }
    ```
  - `404 Not Found`: 
    ```json
    {
      "error": "No data available for the report."
    }
    ```
