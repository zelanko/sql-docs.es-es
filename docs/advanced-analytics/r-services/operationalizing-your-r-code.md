---
title: "Operationalizing Your R Code (Operacionalizaci&#243;n del c&#243;digo R) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f15696b1-2479-4e5f-ac5e-4beaf958a043
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# Operationalizing Your R Code (Operacionalizaci&#243;n del c&#243;digo R)
  A los desarrolladores de bases de datos se les encarga integrar diversas tecnologías y aunar los resultados para que se puedan compartir en toda la empresa. Estos profesionales trabajan con desarrolladores de aplicaciones, programadores de SQL y científicos de datos para diseñar soluciones, recomendar métodos de administración de datos, así como idear e implementar soluciones. [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] ofrece numerosas ventajas para desarrolladores que trabajen con científicos de datos:  
  
-   **Interactuar con secuencias de comandos de R mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].** Aplicación y los desarrolladores de base de datos, así como los analistas que crean informes, pueden invocar un script de R llamando desde un procedimiento almacenado del sistema.  
  
     Para obtener más información acerca de la sintaxis básica, vea [sp_execute_external_script & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) y [utilizando código R en T-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md).  
 
    Para obtener un ejemplo de cómo aplicar R extendido del código mediante los procedimientos almacenados, vea [en base de datos de análisis para los desarrolladores de SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md).
  
     La integración con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también significa que se pueden ejecutar scripts de R con [!INCLUDE[tsql](../../includes/tsql-md.md)] e insertar los resultados en la aplicación. Por ejemplo, puede crear un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que ejecute un script de R y, luego, mostrar los gráficos junto con las predicciones en el informe.  
  
-   **Rendimiento y escalabilidad.** Aunque el lenguaje R abierto se sabe que tienen limitaciones, proporciona el paquete de RevoScaleR API [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] pueden operar en conjuntos de datos grandes y beneficiarse de multiproceso, núcleos múltiples, varios procesos cálculos en base de datos.  
  
     Si la solución R usa agregaciones complejas o implica conjuntos de datos de gran tamaño, puede aprovechar los índices de almacén de columnas y las agregaciones en memoria altamente eficaces de SQL y permitir que el código R controle la puntuación y los cálculos estadísticos.  
  
-   **Herramientas de administración y desarrollo estándar.** No se requiere ninguna herramienta adicional para la administración o la implementación; es posible llamar a todos los trabajos de R si se invoca un procedimiento almacenado.  
  
     Además, el mismo código de R que se ejecuta con datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se puede utilizar con otros orígenes de datos, como Hadoop.  
  
 En esta sección se describen los conceptos que se deben comprender para convertir correctamente soluciones R e implementarlas en el entorno de producción con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
## En esta sección

[Trabajar con tipos de datos de R](../../advanced-analytics/r-services/working-with-r-data-types.md)

[Convertir código de R para su uso en los servicios de R](../../advanced-analytics/r-services/converting-r-code-for-use-in-r-services.md)

##  <a name="bkmk_RelatedTasks"></a> Tareas relacionadas  
  
[Afinación de rendimiento para SQL Server R servicios](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
## Vea también  
 [Características y tareas de SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)   
 [sp_execute_external_script & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)  
  
  