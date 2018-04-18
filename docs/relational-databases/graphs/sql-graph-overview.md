---
title: Gráfico de procesamiento con SQL Server y base de datos de SQL de Azure | Documentos de Microsoft
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: graphs
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
caps.latest.revision: 1
author: shkale-msft
ms.author: shkale
manager: craigg
ms.workload: Active
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: cc6951aa90bf71cb415770f30352120a529bcde1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Gráfico de procesamiento con SQL Server y base de datos de SQL Azure
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece capacidades de la base de datos de gráfico para modelar las relaciones de varios a varios. Las relaciones de gráfico se integran en [!INCLUDE[tsql-md](../../includes/tsql-md.md)] y recibir las ventajas de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como el sistema de administración de base de datos fundamentales.


## <a name="what-is-a-graph-database"></a>¿Qué es una base de datos de gráfico?  
Una base de datos de gráfico es una colección de nodos (o vértices) y bordes (o relaciones). Un nodo representa una entidad (por ejemplo, una persona o una organización) y un borde representa una relación entre los dos nodos que se conecte (por ejemplo, similares o amigos). Nodos y bordes pueden tener propiedades asociadas a ellos. Estas son algunas características que hacen que una base de datos de gráfico único:  
-   Bordes o las relaciones son entidades de primera clases en una base de datos del gráfico y pueden tener asociados atributos o propiedades con ellos. 
-   Un solo borde con flexibilidad puede conectarse a varios nodos en una base de datos del gráfico.
-   Puede expresar coincidencia de patrones y las consultas de navegación de saltos múltiples fácilmente.
-   Puede expresar consultas polimórficas y cierre transitivo fácilmente.

## <a name="when-to-use-a-graph-database"></a>Cuándo se debe utilizar una base de datos de gráfico

No hay nada se que puede conseguir una base de datos de gráfico, que no se puede alcanzar con una base de datos relacional. Sin embargo, una base de datos de gráfico facilitan la express cierto tipo de consultas. Además, con optimizaciones específicas, pueden funcionar mejor determinadas consultas. Su decisión para elegir una frente a otra puede basarse en los siguientes factores:  
-   La aplicación tiene los datos jerárquicos. El tipo de datos HierarchyID puede usarse para implementar las jerarquías, pero tiene algunas limitaciones. Por ejemplo, no permite almacenar varios elementos primarios de un nodo.
-   La aplicación tiene relaciones de varios a varios complejas; a medida que evoluciona la aplicación, se agregan nuevas relaciones.
-   Debe analizar los datos conectadas entre sí y las relaciones.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Características de gráfico presentadas en [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Estamos comenzando agregar extensiones de gráfico a SQL Server, para facilitar la creación de consultas y almacenar datos de gráfico. Las características siguientes se introducen en la primera versión. 


### <a name="create-graph-objects"></a>Crear objetos de gráfico
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] las extensiones le permitirán a los usuarios crear tablas de borde o nodo. Nodos y bordes pueden tener propiedades asociadas a ellos. Desde entonces, nodos y bordes se almacenan como tablas, se admiten todas las operaciones que se admiten en tablas relacionales en la tabla de nodo o borde. A continuación se muestra un ejemplo:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![tablas de amigos persona](../../relational-databases/graphs/media/person-friends-tables.png "nodo Person y amigos arista tablas")  
Nodos y bordes se almacenan como tablas  

### <a name="query-language-extensions"></a>Extensiones de lenguaje de consulta  
Nueva `MATCH` cláusula se introdujo para admitir la coincidencia de patrones y la navegación de salto múltiples a través del gráfico. El `MATCH` función usa la sintaxis de estilo de arte ASCII para la coincidencia. Por ejemplo:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Totalmente integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor 
Extensiones de Graph se integran completamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor. Se usan el mismo motor de almacenamiento, metadatos, procesador de consultas, etc. para almacenar y consultar los datos del gráfico. Esto permite a los usuarios consultar a través de su gráfico y los datos relacionales en una única consulta. Los usuarios también pueden beneficiarse de la combinación de las capacidades del gráfico con otros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologías como servicios de almacén de columnas, de alta disponibilidad, R, etcetera. Base de datos SQL graph también admite todas las seguridad y cumplimiento de normas características disponibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Herramientas y contribuir al ecosistema  
Los usuarios se benefician de las herramientas existentes y contribuir al ecosistema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece. Herramientas como copia de seguridad y restauración, importación y exportación, simplemente funcionen BCP de fábrica. Otras herramientas o servicios como SSIS, SSRS o Power BI funcionará con tablas de gráfico, solo la forma en que trabajan con tablas relacionales.
 
 ## <a name="next-steps"></a>Pasos siguientes  
Leer la [base de datos de gráfico SQL - arquitectura](./sql-graph-architecture.md)
   

