# Proyecto Sprint 8
## Automatización de pruebas — API "Urban Grocers"
Por: Karen Lozano

## Producto o funcionalidad evaluada
Endpoint de creación de kits de la API de Urban Grocers (`POST /api/v1/kits/`), específicamente la validación del parámetro `name` en el cuerpo de la solicitud.

## Objetivo del proyecto
Automatizar pruebas positivas y negativas sobre el parámetro `name` para verificar que el backend aplique correctamente sus propias reglas de validación (longitud permitida, tipo de dato, presencia del campo) antes de crear un kit.

## Tipos de pruebas realizadas
Se automatizaron 9 pruebas basadas en una lista de comprobación:

**Casos positivos (se espera HTTP 201):**
- Nombre con 1 carácter (longitud mínima)
- Nombre con 511 caracteres (longitud máxima permitida)
- Nombre con caracteres especiales
- Nombre con espacios
- Nombre compuesto solo por números, enviado como string

**Casos negativos (se espera HTTP 400):**
- Nombre vacío (0 caracteres)
- Nombre con 512 caracteres (excede el límite permitido)
- Parámetro `name` ausente en el cuerpo de la solicitud
- Parámetro `name` enviado como tipo numérico en lugar de string

## Herramientas utilizadas
- Python
- Pytest
- Requests (para enviar las solicitudes HTTP)
- PyCharm (IDE)
- Git y GitHub

## Documentación generada
- Script de pruebas automatizadas (`create_kit_name_kit_test.py`)
- Módulo de configuración con la URL base y endpoints (`configuration.py`)
- Módulo de datos de prueba, con los 9 casos definidos (`data.py`)
- Módulo de funciones para el envío de solicitudes y obtención de token (`sender_stand_request.py`)
- Este README como documentación del proyecto

## Bugs y hallazgos relevantes
Las 5 pruebas positivas pasaron exitosamente. Sin embargo, **las 4 pruebas negativas detectaron bugs reales en la API**: en los 4 casos (nombre vacío, nombre de 512 caracteres, parámetro `name` ausente y `name` con tipo de dato numérico), la API no devolvió el código de error esperado (400) y en su lugar aceptó las entradas inválidas. Esto indica que el backend no está aplicando correctamente sus propias reglas de validación en la creación de kits.

## Qué aprendí / qué mejoraría
Este proyecto me dejó claro el valor real de las pruebas negativas: no bastaba con confirmar que el endpoint funciona con datos válidos, fue justo al probar los límites y las entradas inválidas donde aparecieron los bugs. Como siguiente paso, documentaría cada uno de estos 4 hallazgos en un reporte formal de bugs (por ejemplo en Jira), con el código de respuesta exacto obtenido, el cuerpo de la respuesta y los pasos para reproducirlo, para poder dar seguimiento con el equipo de desarrollo.

## Instalación
```sh
pip3 install pytest
pip3 install requests
```

## Ejecución de pruebas
```sh
pytest create_kit_name_kit_test.py -v
```
