# Kaiken

Este repositorio fue creado para documentar las decisiones tomadas en el proyecto, el cual vive en **Power BI** y **Google Sheets**.

---

## Accesos

1. **Power BI**: [Ver dashboard](https://app.powerbi.com/view?r=eyJrIjoiMjUyNTlmMzEtMGY4Zi00YjUyLWIxZTYtNWVlZmM3OTg5ZmY5IiwidCI6IjJmMmEwYjI0LWJlYjEtNGE4NS04YTA4LTU4OGNlZWNmNzFkZiJ9)
2. **Google Sheets**: [Ver hoja de cálculo](https://docs.google.com/spreadsheets/d/1e5UGdGPaFLLPG9J4WAKXL7illtta3jfWE2QCHe4-JtM/edit?gid=2143003523#gid=2143003523)

---

## Modelo de datos en Power BI

<img width="787" height="698" alt="Modelo de datos" src="https://github.com/user-attachments/assets/fc032b0f-5de6-4acd-96ba-c0c1f2bcc694" />

---

## Herramientas usadas

- **BigQuery**
- **Cloud Function**
- **Google Sheets**
- **AppScript**
- **Power BI**

---

## Método de uso

1. En **Power BI** puedes visualizar las gráficas.  
   Estas se actualizan diariamente a las **9:00 AM**, aunque se pueden configurar más frecuencias según necesidades del negocio.

2. En **Google Sheets**, los accionables se realizan a través de la pestaña **"Acción"**:  
   <img width="1332" height="468" alt="Acción" src="https://github.com/user-attachments/assets/e152a1d7-e7ef-4704-a7b4-2d0c938e53bc" />

3. Se recomienda partir con:  
   **`Importar Datos → Import all missing sheets`**  
   Esto traerá todas las tablas desde BigQuery.  
   > ⚠️ Esta opción es solo para visualización, no modifica la base de datos.

4. Para **agregar información** (ej: productos con stock, clientes, licitaciones, etc.), utiliza la pestaña **"Agregar"**.

5. Para **editar información** (ej: stock o precio de algún producto), utiliza la pestaña **"Editar"**.

6. Para **actualizar datos** desde la base de datos al Google Sheet:  
   - Presiona **"Actualizar"**  
   - Selecciona la tabla deseada  
   Esto ejecutará un trigger que actualizará la pestaña correspondiente en Google Sheets.

---
