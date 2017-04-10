---
title: "Lesson 2: View and Explore the Data (Data Science End-to-End Walkthrough) (Lecci&#243;n 2: Ver y explorar los datos (Tutorial integral de ciencia de datos)) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 26
---
# Lesson 2: View and Explore the Data (Data Science End-to-End Walkthrough) (Lecci&#243;n 2: Ver y explorar los datos (Tutorial integral de ciencia de datos))
La exploración de datos es una parte importante del modelado de datos e implica la revisión de resúmenes de objetos de datos que se usarán para el análisis, así como la visualización de datos. En esta lección, podrá explorar los objetos de datos y generar gráficos, usando tanto [!INCLUDE[tsql](../../includes/tsql-md.md)] como las funciones de R incluidas en [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
Después, generará trazados para visualizar los datos, mediante las nuevas funciones proporcionadas por los paquetes instalados con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
> [!TIP]  
> ¿Ya es un maestro de R?  
>   
> Ahora que ha descargado todos los datos y ha preparado el entorno, puede ejecutar el script de R completo en RStudio o cualquier otro entorno, y explorar la funcionalidad por su cuenta. Simplemente abra el archivo RSQL_Walkthrough.R y resalte y ejecute líneas individuales, o ejecute el script completo como una demostración.  
>   
> Para obtener explicaciones adicionales de las funciones de RevoScaleR y sugerencias para trabajar con datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en R, continúe con el tutorial. Usa exactamente el mismo script.  
  
## <a name="verify-downloaded-data-using-sql"></a>Comprobar los datos descargados mediante SQL  
En primer lugar, tómese un minuto para asegurarse de que los datos se han cargado correctamente.  
  
1.  Conéctese a su instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    Puede usar diversas herramientas para conectarse y ver bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]    
    -   Explorador de soluciones en Visual Studio  
  
2.  Expanda la base de datos que creó. La siguiente imagen muestra la nueva base de datos, las tablas y las funciones en el **Explorador de servidores.**  
  
    ![new database objects created by script](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG "new database objects created by script")  
  
3.  También puede ejecutar consultas simples en los datos. Por ejemplo, en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic con el botón derecho en la tabla y seleccione **Seleccionar las primeras 1000 filas** para generar y ejecutar esta consulta:  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    Si no ve datos en la tabla, consulte la sección [Solucionar problemas](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md) del tema anterior.
      
4.  Para ver los tipos de datos y el esquema de los datos, puede usar las vistas de administración del sistema en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```  
    SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
    FROM [TaxiSample].INFORMATION_SCHEMA.COLUMNS  
    WHERE TABLE_NAME = N'nyctaxi_sample';  
    ```  
  
    > [!TIP]  
    > Para obtener detalles sobre cómo se creó la tabla de datos, también puede revisar el script `create-db-tb-upload-data.sql`.  
  
### <a name="generate-summaries-using-sql"></a>Generar resúmenes mediante SQL  
Uno de los puntos fuertes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que lo convierte en un buen complemento para R es la capacidad para realizar cálculos basados en conjuntos con mucha rapidez.  El código que creó la tabla de este tutorial también aplica un [índice de almacén de columnas](../Topic/Columnstore%20Indexes%20Guide.md) para realizar cálculos incluso más rápidos.   
  
```  
SELECT DISTINCT [passenger_count]  
    , ROUND (SUM ([fare_amount]),0) as TotalFares   
    , ROUND (AVG ([fare_amount]),0) as AvgFares  
FROM [dbo].[nyctaxi_sample]  
GROUP BY [passenger_count]   
ORDER BY  AvgFares desc  
```  

En el paso siguiente, usará R para generar resúmenes y trazados más sofisticados con los datos de SQL Server.  
  
## <a name="next-steps"></a>Pasos siguientes  
[Ver y resumir datos mediante R &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/view-and-summarize-data-using-r-data-science-end-to-end-walkthrough.md)  
  
[Crear gráficos y trazados con R &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lección anterior  
[Lección 1: Preparar los datos &#40;Tutorial integral de ciencia de datos&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>Vea también  
[Guía de índices de almacén de columnas](../Topic/Columnstore%20Indexes%20Guide.md)  
  
  
  
