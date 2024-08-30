# Umbraco web-app requirements
This document outlines the requirements for the development of a simple web application and its corresponding backend API. The application is an Angular-based web app that interacts with a backend hosted on Google Cloud. The communication between the frontend and backend should utilize HTTP/2 or HTTP/3 protocols, and the data exchanged between them is structured in JSON format.

## Overview
The application is built using Angular version 17.0.6. It allows users to add, prioritize, and select languages. The selected languages will be used by the frontend to fetch translations for use in the app's UI. The backend API consists of two endpoints that provide language data to the frontend.

## Backend
**Endpoint 1:** `/translate/currentLanguageIsoCodeString` 
Functionality: This endpoint returns translation prompts based on the current language ISO code.
Sample response:
```json
{
    "SortLanguagesPrompt": "Sort and add the languages you can read, in order of preference:",
    "ChoosePreferredLanguagesPrompt": "Add more?",
    "NextButtonText": "Next"
}
```
**Endpoint 2:** `/allLanguages/currentCultureIsoCodeString`
Functionality: This endpoint returns all available and supported languages, with a focus on the specified culture ISO code. The culture ISO code input may be redundant in the current app but could be relevant for future backend state management.
Sample response:
```json
{
    "da": {
        "isSelected": true,
        "languageIsoCodesWithLocales": {
            "da": "dansk",
            "da-DK": "dansk - Danmark (Denmark)",
            "da-GL": "dansk - Grønland (Greenland)"
        }
    }
}
```
Note: If the input ISO code is unsupported, the endpoint defaults to English and still returns a 200 OK status.

## Frontend
Users can add as many languages as they want. The first language in the list becomes the active language, which is used to fetch UI translations. The list of added languages can be reordered via drag-and-drop functionality. Each language also allows the selection of a specific region from a dropdown menu.

Users can search for languages. Multiple languages can be selected at once using checkboxes.

## Other requirements
The backend must be resilient against common injection attacks. Any unsupported input should be handled gracefully, defaulting to a standard language without exposing vulnerabilities.

_Possibly performance and scalability requirements_
