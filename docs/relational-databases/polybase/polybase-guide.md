---
title: Guía de PolyBase | Microsoft Docs
ms.date: 05/31/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: polybase
ms.tgt_pltfrm: ''
ms.topic: quickstart
f1_keywords:
- PolyBase
- PolyBase, guide
helpviewer_keywords:
- PolyBase
- PolyBase, overview
- Hadoop import
- Hadoop export
- Hadoop export, PolyBase overview
- Hadoop import, PolyBase overview
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c31f9538f3429ff4ae1182ee0cd974996cc705a6
ms.sourcegitcommit: 82bb56269faf3fb5dd1420418e32a0a6476780cc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/05/2018
ms.locfileid: "43694728"
---
# <a name="polybase-guide"></a>Guía de PolyBase

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]

PolyBase permite que la instancia de SQL Server 2016 procese consultas Transact-SQL que leen datos de Hadoop. La misma consulta también puede acceder a las tablas relacionales de SQL Server. PolyBase permite que la misma consulta también combine los datos de Hadoop y SQL Server. En SQL Server, una [tabla externa](../../t-sql/statements/create-external-table-transact-sql.md) o un [origen de datos externo](../../t-sql/statements/create-external-data-source-transact-sql.md) proporciona la conexión a Hadoop.

PolyBase proporciona estas mismas funcionalidades para los siguientes productos SQL de Microsoft:

- SQL Server 2016 y versiones posteriores
- Analytics Platform System (anteriormente Almacenamiento de datos paralelos)
- Almacenamiento de datos SQL de Azure

PolyBase inserta algunos cálculos en el nodo de Hadoop para optimizar la consulta global. Sin embargo, el acceso externo de PolyBase no se limita a Hadoop. También se admiten otras tablas no relacionales no estructuradas, como archivos de texto delimitado.

#### <a name="data-import-and-export"></a>Importación y exportación de datos

Con la ayuda de PolyBase, las consultas T-SQL también pueden importar y exportar datos desde Azure Blob Storage. Además, PolyBase permite a Azure SQL Data Warehouse importar y exportar datos desde Azure Data Lake Store y Azure Blob Storage.

Para usar PolyBase, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).
  
![Lógica de PolyBase](../../relational-databases/polybase/media/polybase-logical.png "Lógica de PolyBase")

## <a name="why-use-polybase"></a>Por qué usar PolyBase

En el pasado era más difícil combinar los datos de SQL Server con datos externos. Tenía las dos opciones desagradables siguientes:

- Transferir la mitad de sus datos de modo que todos sus datos estuvieran en un formato u otro.
- Consultar ambos orígenes de datos, después escribir una lógica de consulta personalizada para combinar e integrar los datos en el nivel de cliente.

PolyBase evita esas opciones mediante el uso de Transact-SQL para combinar los datos

Por simplificar, PolyBase no requiere que instale más software en el entorno de Hadoop. Los datos externos se consultan mediante la misma sintaxis T-SQL que se utiliza para consultar una tabla de base de datos. Las acciones de asistencia implementadas por PolyBase son transparentes. El autor de la consulta no necesita ningún conocimiento sobre Hadoop.

PolyBase hace lo siguiente:

- **Consultar datos almacenados en Hadoop desde SQL Server o PDW.** Los usuarios almacenan datos en sistemas rentables, distribuidos y escalables, como Hadoop. PolyBase facilita la consulta de datos mediante T-SQL.

- **Consultar datos almacenados en Azure Blob Storage.** El almacenamiento de blobs de Azure es un lugar muy cómodo donde almacenar datos para que los usen los servicios de Azure.  PolyBase facilita el acceso a los datos mediante T-SQL.

- **Importación de datos desde Hadoop, Azure Blob Storage o Azure Data Lake Store** Saque partido de la velocidad de la tecnología de almacén de columnas y las capacidades de análisis de Microsoft SQL e importe datos desde Hadoop, Azure Blob Storage o Azure Data Lake Store en tablas relacionales. No es necesaria ninguna herramienta independiente de ETL o de importación.

- **Exportar datos a Hadoop, Azure Blob Storage o Azure Data Lake Store** Archive datos en Hadoop, Azure Blob Storage o Azure Data Lake Store para disfrutar de un almacenamiento rentable y mantenerlo en línea para un fácil acceso.

- **Integrarse con herramientas de BI.** Use PolyBase con la pila de análisis y la inteligencia empresarial de Microsoft o recurra a cualquier herramienta de terceros que sea compatible con SQL Server.

## <a name="performance"></a>Rendimiento

- **Inserción de cálculo en Hadoop.** El optimizador de consultas toma una decisión basada en costos para insertar cálculo en Hadoop cuando, al hacerlo, se va a mejorar el rendimiento de las consultas.  Para tomar esa decisión basada en costos, usa estadísticas relativas a las tablas externas. La inserción de cálculo crea trabajos MapReduce y aprovecha los recursos de cálculo distribuidos de Hadoop.

- **Escala de los recursos de cálculo.** Para mejorar el rendimiento de las consultas, puede usar [grupos de escalado horizontal de PolyBase](../../relational-databases/polybase/polybase-scale-out-groups.md)de SQL Server. Gracias a esto, la transferencia de datos paralelos entre instancias de SQL Server y nodos de Hadoop es factible y, además, se agregan recursos de cálculo para operar en los datos externos.

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
| &nbsp; | &nbsp; |
  
