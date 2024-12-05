# Testy jednostkowe i integracyjne dla projektu

## Przykładowe Testy jednostkowe

### 1. User
- **Test logowania (`login`)**:
    - **Wejście**: poprawna nazwa użytkownika i hasło.
    - **Oczekiwane wyjście**: pomyślne zalogowanie i wygenerowanie sesji użytkownika.
    - **Przypadki graniczne**: nieprawidłowe dane logowania, puste pola.

- **Test zmiany hasła (`changePassword`)**:
    - **Wejście**: poprawne stare hasło i nowe hasło.
    - **Oczekiwane działanie**: aktualizacja hasła użytkownika w bazie danych.
    - **Przypadki**: próba zmiany hasła bez uwierzytelnienia.

### 2. System powiadomień (NotificationManager)
- **Test generowania alertów (`generateAlerts`)**:
    - **Wejście**: dane o zachorowaniach przekraczające próg krytyczny.
    - **Oczekiwane wyjście**: utworzenie alertu o poprawnym formacie.

- **Test dostosowywania ustawień powiadomień (`customizeNotificationSettings`)**:
    - **Wejście**: zmiana parametrów notyfikacji (próg, typ).
    - **Oczekiwane działanie**: poprawna aktualizacja ustawień w systemie.

### 3. Model uczenia maszynowego (MachineLearningModel)
- **Test trenowania modelu (`trainModel`)**:
    - **Wejście**: zbiór danych treningowych.
    - **Oczekiwane działanie**: model trenuje się poprawnie i zapisuje parametry.
    - **Przypadki**: brakujące dane w zbiorze.

- **Test predykcji (`predict`)**:
    - **Wejście**: poprawny zbiór testowy.
    - **Oczekiwane wyjście**: poprawny wynik predykcji z wysoką dokładnością.

---

## Przykładowe Testy integracyjne

### 1. Integracja `User` z `NotificationManager`
- **Cel**: Sprawdzenie, czy użytkownik może dostosować powiadomienia i otrzymywać je zgodnie z ustawieniami.
- **Wejście**: próg alertów zmieniony przez użytkownika.
- **Oczekiwane działanie**: alerty generowane zgodnie z nowymi ustawieniami.

### 2. Integracja `DataCollector` z `Database` i `DataPreprocessor`
- **Cel**: Sprawdzenie przepływu danych od pobrania, przez przetworzenie, aż do zapisania w bazie.
- **Wejście**: źródło danych (CSV, API).
- **Oczekiwane działanie**: poprawne przetworzenie i zapisanie danych w bazie.

### 3. Integracja `MachineLearningModel` z aplikacją webową (`WebApplication`)
- **Cel**: Sprawdzenie, czy predykcje modelu są poprawnie wyświetlane w UI.
- **Wejście**: dane wejściowe dla modelu.
- **Oczekiwane działanie**: użytkownik otrzymuje wynik predykcji w interfejsie.

---

## Rekomendowane narzędzia testowe

### 1. Backend (Python/Django/TensorFlow)
- **Testy jednostkowe**:
    - **Pytest**: wszechstronne i łatwe w użyciu narzędzie do pisania testów jednostkowych.
    - **Unittest**: wbudowane w Python narzędzie, które również sprawdzi się do testów.

- **Testy integracyjne**:
    - **Django Test Framework**: wbudowany framework do testowania aplikacji opartych na Django.
    - **Postman + Newman**: do testowania API.

### 2. Frontend (React.js)
- **Testy jednostkowe**:
    - **Jest**: domyślne narzędzie do testowania React.js.
    - **React Testing Library**: do testowania komponentów UI.

### 3. Model uczenia maszynowego (TensorFlow)
- **Testy jednostkowe**:
    - **TensorFlow Testing Utilities**: wbudowane narzędzia do weryfikacji działania modelu.

- **Testy modelu**:
    - **MLflow**: do monitorowania i walidacji modelu (opcjonalnie).

### 4. Baza danych (PostgreSQL)
- **Testy integracyjne**:
    - **pytest-django**: rozszerzenie do Pytesta obsługujące testy z PostgreSQL.
    - **pgTAP**: framework do testowania baz danych PostgreSQL.
