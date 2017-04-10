---
title: "Escenarios de ciencia de datos y plantillas de soluciones | Microsoft Docs"
ms.custom: ""
ms.date: "04/18/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 49e54fa9-9b28-44ba-b256-06dad4e8dece
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# Escenarios de ciencia de datos y plantillas de soluciones
Las plantillas son soluciones de ejemplo que muestran los procedimientos recomendados y proporcionan los bloques de creación para ayudarle a implementar una solución rápida. Cada plantilla está diseñada para resolver un problema específico e incluye datos de ejemplo, código de R (Microsoft R Server) y procedimientos almacenados de SQL. Las tareas de cada plantilla permiten desde preparación de datos e ingeniería de características hasta el entrenamiento y la puntuación de modelos. El código se puede ejecutar en un IDE de R realizando los cálculos en SQL Server, o mediante una herramienta cliente de SQL como SQL Server Management Studio.  
  
Puede usar estas plantillas para aprender cómo funciona [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] y crear e implementar su propia solución personalizando la plantilla para ajustarla a su propio escenario.  
  
Para obtener instrucciones de descarga y configuración, consulte [Cómo usar las plantillas](#bkmk_HowTo) al final de este tema.  
  
## Detección de fraude  
[Plantilla de detección de fraude en línea (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/FraudDetection/Introduction.md)  
  
Una de las tareas importantes para las empresas en línea es detectar transacciones fraudulentas e identificar las transacciones realizadas por instrumentos o credenciales de pago robados, con el fin de reducir las pérdidas de cancelación de cargos. Cuando se detectan transacciones fraudulentas, las empresas suelen adoptar medidas para bloquear determinadas cuentas tan pronto como sea posible, para evitar pérdidas mayores. En este escenario, aprenderá a usar los datos de las transacciones de compra en línea para identificar posibles fraudes. Esta metodología se puede aplicar fácilmente a la detección de fraude en otros dominios.  
  
En esta plantilla aprenderá a usar los datos de las transacciones de compra en línea para identificar posibles fraudes. La detección de fraude se resuelve como un problema de clasificación binaria. La metodología empleada en esta plantilla se puede aplicar fácilmente a la detección de fraude en otros dominios.    
  
## Abandono de clientes  
[Plantilla de predicción de abandono de clientes (SQL Server R Services)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/Churn/Introduction.md)  
  
El análisis y la predicción del abandono de clientes es importante en cualquier sector donde debe administrarse y evitar la pérdida de clientes a los competidores: banca, telecomunicaciones y comercial, por nombrar algunos. El objetivo del análisis del abandono es identificar qué clientes tienen probabilidades de abandonar y después adoptar las acciones adecuadas para conservar a esos clientes y mantener su negocio.  
  
Esta plantilla le ayudará a comenzar con la prevención del abandono mediante la formulación del problema como un problema de **clasificación binaria**. Usa datos de ejemplo de dos orígenes, datos demográficos y transacciones del cliente, para clasificar a los clientes como con probabilidad de abandono o poca probabilidad de abandono.   
  
## Mantenimiento predictivo  
[Plantilla de mantenimiento predictivo (SQL Server 2016)](https://github.com/Microsoft/SQL-Server-R-Services-Samples/blob/master/PredictiveMaintenance/Introduction.md)  
  
El objetivo de un mantenimiento predictivo "controlado por datos" es aumentar la eficiencia de las tareas de mantenimiento mediante la captura de errores del pasado y el uso de esa información para predecir cuándo o dónde se puede producir un error en un dispositivo. La capacidad de previsión de la obsolescencia de los dispositivos es especialmente importante para las aplicaciones que dependen de datos distribuidos o sensores, como ejemplifica el Internet de las cosas (IoT).  
  
Esta plantilla se centra en responder a la pregunta "¿Cuándo se producirá un error en un equipo en activo?". Los datos de entrada representan medidas de sensor simuladas para motores de avión. Los datos obtenidos de la supervisión de las condiciones de funcionamiento actuales del motor, como el ciclo de trabajo actual, ajustes, medidas de sensor y así sucesivamente, se usan para crear tres tipos de modelos de predicción:  
  
-   **Modelos de regresión**, para predecir cuánto tiempo durará un motor antes de que se produzca un error. El modelo de ejemplo predice la métrica Vida útil restante (RUL), también denominada Tiempo hasta el fallo (THF).  
  
-   **Modelos de clasificación**, para predecir si un motor es propenso a errores.  
  
    El **modelo de clasificación binaria** predice si producirá un error en un motor en un determinado período de tiempo (número de días).  
  
    El **modelo de clasificación multiclase** predice si se producirá un error en un motor concreto y, si se produce, proporciona una ventana de tiempo probable del error. Por ejemplo, para un día determinado, puede predecir si es probable que se produzca un error en un dispositivo en el día especificado o en un periodo de tiempo después de ese día.  
      
      
## Previsión de demanda de energía  
[Plantilla de previsión de demanda de energía con SQL Server R Services](https://gallery.cortanaintelligence.com/Tutorial/Energy-Demand-Forecast_Template_with_SQL-Server-R-Services-1)  
  
Esta plantilla muestra cómo usar SQL Server R Services para predecir la demanda de electricidad. La solución incluye un simulador de demanda, todo el código de R y T-SQL necesario para entrenar un modelo y los procedimientos almacenados que puede usar para generar y presentar las predicciones.   
  
## <a name="bkmk_HowTo"></a>Cómo utilizar las plantillas  
Para descargar los archivos incluidos en cada plantilla, puede usar los comandos de GitHub o puede abrir el vínculo y hacer clic en **Descargar Zip** para guardar todos los archivos en el equipo.  Una vez descargada, la solución suele contener estas carpetas:  
  
-   **Data**: contiene los datos de ejemplo para cada aplicación.  
  
-   **R**: contiene todo el código de desarrollo de R que necesita para la solución. La solución requiere las bibliotecas proporcionadas por Microsoft R Server, pero también se puede abrir y editar en cualquier IDE de R. El código de R se ha optimizado para que los cálculos se realicen "en la base de datos", al establecer el contexto de cálculo en una instancia de SQL Server.  
  
-   **SQLR**: contiene varios archivos .sql que se pueden ejecutar en un entorno de SQL como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear los procedimientos almacenados que realizan tareas relacionadas como procesamiento de datos, ingeniería de características e implementación de modelos.  
  
    La carpeta también contiene un script de PowerShell que puede ejecutar para invocar todos los scripts y crear el entorno integral.  
  
    Asegúrese de editar el script para que se adapte a su entorno.  
  
  
## Vea también  
[Tutoriales de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
[Anuncio de las plantillas en Azure ML](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
[Nueva plantilla de mantenimiento predictivo](https://blogs.technet.microsoft.com/machinelearning/2015/04/09/exciting-new-templates-in-azure-ml/)  
  
  
  
