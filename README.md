Descripción
-----------
Proyecto de análisis de consumo para Megaline con el objetivo de determinar cuál de las dos tarifas prepago (Surf vs Ultimate) genera más ingresos a partir de una muestra de 500 clientes durante 2018.

Objetivo
--------
- Limpiar y preparar los datos (llamadas, mensajes, internet, planes y usuarios).
- Agregar el consumo por usuario y mes.
- Calcular los ingresos mensuales por usuario según las condiciones de cada plan.
- Comparar las tarifas y generar conclusiones para decisión comercial.

Estructura del repositorio / Notebook
-------------------------------------
- Notebook (Jupyter): secciones para inicialización, carga y limpieza de datos, enriquecimiento, agregación por usuario/mes, cálculo de ingresos y análisis exploratorio.
- /datasets/
    - megaline_calls.csv
    - megaline_internet.csv
    - megaline_messages.csv
    - megaline_plans.csv
    - megaline_users.csv

Requisitos
----------
- Python 3.7+
- pandas
- numpy
- matplotlib
- seaborn
- scipy

Instalación (ejemplo con pip)
-----------------------------
pip install pandas numpy matplotlib seaborn scipy

Cómo ejecutar
-------------
1. Abrir el notebook en JupyterLab/Jupyter Notebook.
2. Ejecutar las celdas en orden (la notebook asume que los CSV están en /datasets/).
3. Revisar las secciones:
     - Inicialización
     - Carga de datos
     - Correcciones (fechas, conversión de tipos)
     - Enriquecimiento (mes, año)
     - Agregación por usuario y mes
     - Cálculo de ingresos mensuales por usuario
     - Análisis por plan (estadísticas y gráficas)

Metodología (resumen)
---------------------
- Conversión de columnas de fecha a datetime.
- Enriquecimiento de tablas con columnas month/year.
- Agregación mensual por user_id de llamadas (cantidad y minutos), mensajes y MB de internet.
- Composición de una tabla mensual por usuario uniendo datos de consumo y detalles del plan.
- Cálculo de ingresos mensuales:
    - Se suma la cuota mensual del plan.
    - Si consumo > incluido, se calcula sobrecargo:
        - Llamadas: minutos excedentes * usd_per_minute
        - Mensajes: mensajes excedentes * usd_per_message
        - Datos: MB excedentes convertidos a GB (1 GB = 1024 MB), redondeando hacia arriba con np.ceil, * usd_per_gb
- Visualizaciones: series mensuales, histogramas y boxplots por plan para minutos, mensajes y datos.

Supuestos y notas
-----------------
- Conversión MB → GB usa factor 1024 MB = 1 GB.
- Las llamadas con duración 0 pueden filtrarse si se considera que no aportan valor (se dejó como nota en el notebook).
- Redondeo de GB excedentes hacia arriba (np.ceil) para cálculo de cargos por datos.
- Fechas de baja (churn_date) se parsean con errors='coerce' para manejar valores vacíos.

Resultados principales (resumen)
-------------------------------
- Se calcularon ingresos mensuales por usuario y se compararon por plan.
- Visualizaciones y estadísticas descriptivas permiten observar diferencias de comportamiento entre Surf y Ultimate en llamadas, mensajes y consumo de datos.
- Con base en los ingresos agregados (ver sección de análisis del notebook) se puede determinar qué plan genera más ingreso promedio por usuario y total.
