---
title: "Guía de PolyBase | Microsoft Docs"
ms.date: 5/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: get-started-article
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- "Hadoop import ×"
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
ms.assetid: b42b7d48-328a-4046-abe9-f73fd83212dc
caps.latest.revision: 26
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 3fc2a681f001906cf9e819084679db097bca62c7
ms.openlocfilehash: f9fe99ddd630b8444819c94111f6a363e96105f5
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="polybase-guide"></a>Guía de PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  PolyBase es una tecnología que tiene acceso a datos fuera de la base de datos mediante el lenguaje de t-SQL.  En SQL Server 2016, permite ejecutar consultas en datos externos en Hadoop o para importar o exportar datos desde el almacenamiento de blobs de Azure. Las consultas se optimizan para insertar cálculo en Hadoop. En el almacén de datos de SQL Azure, se pueden importar/exportar datos desde el almacenamiento de blobs de Azure y almacén de Azure Data Lake.
  
  
 Para usar PolyBase, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
 ![Lógica de PolyBase](../../relational-databases/polybase/media/polybase-logical.png "Lógica de PolyBase")  
  
## <a name="why-use-polybase"></a>Por qué usar PolyBase  
Para tomar las decisiones correctas, necesitará analizar datos relacionales y de otra índole que no están estructurados en tablas (especialmente en Hadoop). Esto es difícil de lograr, a menos que exista una forma de transferir datos entre distintos tipos de almacenes de datos. PolyBase llena este vacío al operar con datos externos a SQL Server.  
  
Para simplificar, PolyBase no requiere instalar software adicional en el entorno de Hadoop. En las consultas de datos externos se usa la misma sintaxis que al consultar una tabla de base de datos. Todo esto ocurre de forma transparente. PolyBase controla todos los detalles en segundo plano y no hay información acerca de Hadoop es necesario que el usuario final para consultar tablas externas. 
  
 PolyBase hace lo siguiente:  
  
-   **Consultar datos almacenados en Hadoop de SQL Server o PDW.** Los usuarios almacenan datos en sistemas rentables, distribuidos y escalables, como Hadoop. PolyBase facilita la consulta de datos mediante T-SQL.  
  
-   **Consultar datos almacenados en almacenamiento de blobs de Azure.** El almacenamiento de blobs de Azure es un lugar muy cómodo donde almacenar datos para que los usen los servicios de Azure.  PolyBase facilita el acceso a los datos mediante T-SQL.  
  
-   **Importar datos de almacén de Data Lake de Azure, almacenamiento de blobs de Azure o Hadoop** aprovechar la velocidad de las capacidades de tecnología y análisis de almacén de columnas de Microsoft SQL mediante la importación de datos de almacén de Data Lake de Azure, almacenamiento de blobs de Azure o Hadoop en tablas relacionales. No es necesaria ninguna herramienta independiente de ETL o de importación.  

-   **Exportar datos a Hadoop, Azure Blob Storage o Azure Data Lake Store** Archive datos en Hadoop, Azure Blob Storage o Azure Data Lake Store para disfrutar de un almacenamiento rentable y mantenerlo en línea para un fácil acceso.  
  
-   **Integrarse con herramientas de BI.** Use PolyBase con la pila de análisis y la inteligencia empresarial de Microsoft o recurra a cualquier herramienta de terceros que sea compatible con SQL Server.  
  
## <a name="performance"></a>Rendimiento  
  
-   **Inserción de cálculo en Hadoop.**El optimizador de consultas toma una decisión basada en costos para insertar cálculo en Hadoop cuando, al hacerlo, se va a mejorar el rendimiento de las consultas.  Para tomar esa decisión basada en costos, usa estadísticas relativas a las tablas externas.   La inserción de cálculo crea trabajos MapReduce y aprovecha los recursos de cálculo distribuidos de Hadoop.  
  
-   **Escala de los recursos de cálculo.** Para mejorar el rendimiento de las consultas, puede usar [grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)de SQL Server. Gracias a esto, la transferencia de datos paralelos entre instancias de SQL Server y nodos de Hadoop es factible y, además, se agregan recursos de cálculo para operar en los datos externos.  
  
## <a name="polybase-guide-topics"></a>Temas de la guía de PolyBase  
 Esta guía incluye temas que sirven para usar PolyBase de forma eficaz.  
  
|||  
|-|-|  
|**Tema**|**Descripción**|  
|[Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md)|Pasos básicos para instalar y configurar PolyBase. Se explica cómo crear objetos externos que apuntan a datos en Hadoop o en un almacenamiento de blobs de Azure y se incluyen ejemplos de consulta.|  
|[Resumen de características de PolyBase con versiones](../../relational-databases/polybase/polybase-versioned-feature-summary.md)|Se describen las características de PolyBase compatibles en SQL Server, Base de datos SQL y Almacenamiento de datos SQL.|  
|[grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)|Paralelismo en el escalado horizontal entre SQL Server y Hadoop por medio del uso de grupos de escalado horizontal de SQL Server.|  
|[Instalación de PolyBase](../../relational-databases/polybase/polybase-installation.md)|Referencia y pasos necesarios para instalar PolyBase con el asistente para la instalación o con una herramienta de línea de comandos.|  
|[Configuración de PolyBase](../../relational-databases/polybase/polybase-configuration.md)|Se describe cómo configurar SQL Server para PolyBase.  Por ejemplo, configurar la inserción de cálculo y la seguridad de Kerberos.|  
|[objetos T-SQL de PolyBase](../../relational-databases/polybase/polybase-t-sql-objects.md)|Se explica cómo crear los objetos de T-SQL que PolyBase usa para definir datos externos y tener acceso a ellos.|  
|[PolyBase Queries](../../relational-databases/polybase/polybase-queries.md)|Se indica cómo usar instrucciones de T-SQL para consultar, importar o exportar datos externos.|  
|[Solución de problemas de PolyBase](../../relational-databases/polybase/polybase-troubleshooting.md)|Técnicas para administrar consultas de PolyBase. Use vistas de administración dinámica para supervisar las consultas de PolyBase y aprenda a leer un plan de consulta de PolyBase para hallar los cuellos de botella de rendimiento.|  
  
  

