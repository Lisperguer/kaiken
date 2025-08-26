# Kaiken

Este repositorio fue creado para documentar las decisiones tomadas en el proyecto, el cual vive en **Power BI** y **Google Sheets**.

---

## Accesos

1. **Power BI**: [Ver dashboard](https://app.powerbi.com/view?r=eyJrIjoiMjUyNTlmMzEtMGY4Zi00YjUyLWIxZTYtNWVlZmM3OTg5ZmY5IiwidCI6IjJmMmEwYjI0LWJlYjEtNGE4NS04YTA4LTU4OGNlZWNmNzFkZiJ9)
2. **Google Sheets**: [Ver hoja de cálculo](https://docs.google.com/spreadsheets/d/1e5UGdGPaFLLPG9J4WAKXL7illtta3jfWE2QCHe4-JtM/edit?gid=2143003523#gid=2143003523)

---

## Modelo de datos en Power BI
Este modelo permite la ingesta de todas lentidades para este proyecto. Además, permite trabajar con stock por producto por proveedor, soportando el esquema de que un proveedor entrega varios productos pero también un producto puede ser entregado por varios proveedores

<img width="787" height="698" alt="Modelo de datos" src="https://github.com/user-attachments/assets/fc032b0f-5de6-4acd-96ba-c0c1f2bcc694" />

---

## Herramientas usadas

- **BigQuery**
- **Cloud Function**
- **Google Sheets**
- **AppScript**
- **Power BI**

¿Porqué estas herramientas?
El ecosistema google permite un sistema simple y probado de seguridad. Solamente pueden ver/editar aquellos que se les comparta el acceso mediante correo. Por lo tanto, las ventajas que tenemos son:
1. No hay que diseñar sistema de autenticación, ya viene integrado.
2. No hay que hostear algún link para las cloud functions, se realiza automáticamente. Las cloud functions se pueden integrar con github para realizar CI/CD de manera nativa, lo cual también acelará el desarrollo a futuro haciéndolo más robusto
3. AppScript (Código en Sheet) viene integrado con Google Sheet, lo que hace más directo el desarrollo. Además, cuenta con versionamiento en caso de querer realizar un rollback
4. BigQuery: para fácil integración con Google Sheets/App Script

Desventajas: 
1. BigQuery no posee modelado de datos, así que en caso de querer realizar una integración con otra plataforma que lo realice, se deberá hacer por código
2. La desventaja anterior se suple con PowerBi, ya que al integrar las tablas de manera nativa podemos relacionarlas entre sí
   

---

## Método de uso

1. En **Power BI** puedes visualizar las gráficas.  
   Estas se actualizan diariamente a las **9:00 AM**, aunque se pueden configurar más frecuencias según necesidades del negocio.
   También, desde Power BI se puede acceder directamente el link de registros, el cuál se logra haciendo "Ctrl + click" sobre el botón del gráfico

3. En **Google Sheets**, los accionables se realizan a través de la pestaña **"Acción"**:  
   <img width="1332" height="468" alt="Acción" src="https://github.com/user-attachments/assets/e152a1d7-e7ef-4704-a7b4-2d0c938e53bc" />

4. Se recomienda partir con:  
   **`Importar Datos → Import all missing sheets`**  
   Esto traerá todas las tablas desde BigQuery.  
   > ⚠️ Esta opción es solo para visualización, no modifica la base de datos.

5. Para **agregar información** (ej: productos con stock, clientes, licitaciones, etc.), utiliza la pestaña **"Agregar"**.

6. Para **editar información** (ej: stock o precio de algún producto), utiliza la pestaña **"Editar"**.

7. Para **actualizar datos** desde la base de datos al Google Sheet:  
   - Presiona **"Actualizar"**  
   - Selecciona la tabla deseada  
   Esto ejecutará un trigger que actualizará la pestaña correspondiente en Google Sheets.
---

## Agregar Tender

** Variables ** 
Al agregar un tender, se pedirá el product_id, provider_id y el cliente_id. Para obtener el product_id y provider_id, se recomienda ir a la pestaña **current_stock_cost** y obtener el product_id y provider_id. Para client_id se recomienda ir a la tabla **clientes** y obtenerlo
<img width="913" height="872" alt="image" src="https://github.com/user-attachments/assets/6ccf060e-5b99-440c-942a-7267c53fe89a" />


**En caso de que no se cumple una condición**
Aparecerá un popup. El Popup tiene un mensaje de respuesta del servidor de bigquery, en donde al final se detallará la razón del rechazo.

<img width="987" height="1046" alt="image" src="https://github.com/user-attachments/assets/4b1357dc-45c3-4213-b897-9d6157786292" />


---

## Aspectos de mejora

Debido a al tiempo dedicado a este MVP, quedan como propuesta las siguientes mejoras:

1. Al momento de agregar un tender, que los productos, proveedores y clientes sean un dropdown con los ya existentes
2. Precargar información de manera constante para que sea más fácil su lectura mediante un Google Scheduler, así no hay necesidad de cargar información
3. Unificar App Script en una cloud function y que se agregue automáticamente a varios Google Sheets, así la mantención se hace en un solo código
4. Crear otra tabla cada vez que hayan cambios en stock/precio. Así, podemos ver la evolución de cada proveedor en el tiempo en cuánto a su stock y precio
