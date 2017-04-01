---
title: "Gu&#237;a de PolyBase | Microsoft Docs"
ms.date: "12/08/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-polybase"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
f1_keywords: 
  - "PolyBase"
  - "PolyBase, guide"
helpviewer_keywords: 
  - "PolyBase"
  - "PolyBase, información general"
  - "importación de Hadoop ×"
  - "exportación de Hadoop"
  - "exportación de Hadoop, información general de PolyBase"
  - "importación de Hadoop, información general de PolyBase"
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: "barbkess"
ms.author: "barbkess"
manager: "jhubbard"
caps.handback.revision: 24
---
# Gu&#237;a de PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase es una tecnología que tiene acceso a los datos relacionales y no relacionales y los combina, todo ello desde SQL Server.   Permite ejecutar consultas sobre datos externos en Hadoop o en un almacenamiento de blobs de Azure.   Las consultas se optimizan para insertar cálculo en Hadoop.  
  
 Únicamente con instrucciones de Transact-SQL (T-SQL), se pueden importar y exportar datos indistintamente entre tablas relacionales en SQL Server, así como datos no relacionales almacenados en Hadoop o un almacenamiento de blobs de Azure. También se pueden consultar datos externos desde una consulta de T-SQL y combinarlos con datos relacionales.  
  
 Para usar PolyBase, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![PolyBase logical](../../relational-databases/polybase/media/polybase-logical.png "PolyBase logical")  
  
## Por qué usar PolyBase  
 Para tomar las decisiones correctas, los responsables de decisiones empresariales necesitan analizar datos relacionales y de otra índole que no están estructurados en tablas (nos estamos refiriendo sobre todo a Hadoop y a otras tecnologías de NoSQL). Esto es difícil de lograr, a menos que exista una forma de transferir datos entre distintos tipos de almacenes de datos. PolyBase llena este vacío al operar con datos externos a SQL Server.  
  
 Por simplificar, PolyBase no requiere instalar más software en el entorno de Azure o Hadoop.         En las consultas de datos externos se usa la misma sintaxis que al consultar una tabla de base de datos. Todo esto ocurre de forma transparente. PolyBase controla todos los detalles en segundo plano y no es necesario tener ningún conocimiento sobre Azure o Hadoop para usarlo correctamente.  
  
 PolyBase hace lo siguiente:  
  
-   **Consultar datos almacenados en Hadoop.** Los usuarios almacenan datos en sistemas rentables, distribuidos y escalables, como Hadoop. PolyBase facilita la consulta de datos mediante T-SQL.  
  
-   **Consultar datos almacenados en un almacenamiento de blobs de Azure.** El almacenamiento de blobs de Azure es un lugar muy cómodo donde almacenar datos para que los usen los servicios de Azure.  PolyBase facilita el acceso a los datos mediante T-SQL.  
  
-   **Importar datos desde Hadoop o un almacenamiento de blobs de Azure.** Saque partido de la velocidad de la tecnología de almacén de columnas y las capacidades de análisis de Microsoft SQL e importe datos desde Hadoop o desde un almacenamiento de blobs de Azure en tablas relacionales. No es necesaria ninguna herramienta independiente de ETL o de importación.  
  
-   **Exportar datos a Hadoop o a un almacenamiento de blobs de Azure.** Archive datos en Hadoop o en un almacenamiento de blobs de Azure para disfrutar de un almacenamiento rentable y mantenerlo en línea para un fácil acceso.  
  
-   **Integrarse con herramientas de BI.** Use PolyBase con la pila de análisis y la inteligencia empresarial de Microsoft o recurra a cualquier herramienta de terceros que sea compatible con SQL Server.  
  
## Rendimiento  
  
-   **Inserción de cálculo en Hadoop.**El optimizador de consultas toma una decisión basada en costos para insertar cálculo en Hadoop cuando, al hacerlo, se va a mejorar el rendimiento de las consultas.  Para tomar esa decisión basada en costos, usa estadísticas relativas a las tablas externas.   La inserción de cálculo crea trabajos MapReduce y aprovecha los recursos de cálculo distribuidos de Hadoop.  
  
-   **Escala de los recursos de cálculo.** Para mejorar el rendimiento de las consultas, puede usar [grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md) de SQL Server. Gracias a esto, la transferencia de datos paralelos entre instancias de SQL Server y nodos de Hadoop es factible y, además, se agregan recursos de cálculo para operar en los datos externos.  
  
## Temas de la guía de PolyBase  
 Esta guía incluye temas que sirven para usar PolyBase de forma eficaz.  
  
|||  
|-|-|  
|**Tema**|**Descripción**|  
|[Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|Pasos básicos para instalar y configurar PolyBase. Se explica cómo crear objetos externos que apuntan a datos en Hadoop o en un almacenamiento de blobs de Azure y se incluyen ejemplos de consulta.|  
|[Resumen de características de PolyBase con versiones](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|Se describen las características de PolyBase compatibles en SQL Server, Base de datos SQL y Almacenamiento de datos SQL.|  
|[Grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)|Paralelismo en el escalado horizontal entre SQL Server y Hadoop por medio del uso de grupos de escalado horizontal de SQL Server.|  
|[Instalación de PolyBase](../../relational-databases/polybase/polybase-installation.md)|Referencia y pasos necesarios para instalar PolyBase con el asistente para la instalación o con una herramienta de línea de comandos.|  
|[Configuración de PolyBase](../../relational-databases/polybase/polybase-configuration.md)|Se describe cómo configurar SQL Server para PolyBase.  Por ejemplo, configurar la inserción de cálculo y la seguridad de Kerberos.|  
|[objetos T-SQL de PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)|Se explica cómo crear los objetos de T-SQL que PolyBase usa para definir datos externos y tener acceso a ellos.|  
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|Se indica cómo usar instrucciones de T-SQL para consultar, importar o exportar datos externos.|  
|[Solución de problemas de PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md)|Técnicas para administrar consultas de PolyBase. Use vistas de administración dinámica para supervisar las consultas de PolyBase y aprenda a leer un plan de consulta de PolyBase para hallar los cuellos de botella de rendimiento.|  
  
  