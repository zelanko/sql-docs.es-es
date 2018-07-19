---
title: Gráfico de procesamiento con SQL Server y Azure SQL Database | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: 8c2ad7f5b31a97de5d0bfb22074b55bd61bb825b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38015681"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Gráfico de procesamiento con SQL Server y Azure SQL Database
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece capacidades de base de datos de gráfico para modelar las relaciones de varios a varios. Las relaciones de graph se integran en [!INCLUDE[tsql-md](../../includes/tsql-md.md)] y recibir las ventajas de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como el sistema de administración de base de datos fundamentales.


## <a name="what-is-a-graph-database"></a>¿Qué es una base de datos de gráfico?  
Una base de datos de gráfico es una colección de nodos (o vértices) y bordes (o relaciones). Un nodo representa una entidad (por ejemplo, una persona o una organización) y un borde representa una relación entre los dos nodos que se conecta (por ejemplo, "Me gusta" o amigos). Los nodos y bordes pueden tener propiedades asociadas a ellos. Estas son algunas características que hacen que una base de datos de gráfico únicos:  
-   Bordes o las relaciones son entidades de primera clases en una base de datos del gráfico y pueden atributos o propiedades asociados a ellas. 
-   Un solo borde flexible puede conectar varios nodos en una base de datos del gráfico.
-   Coincidencia de patrones y las consultas de navegación en saltos múltiples se pueden expresar fácilmente.
-   Puede expresar consultas polimórficas y cierre transitivo fácilmente.

## <a name="when-to-use-a-graph-database"></a>Cuándo usar una base de datos de gráfico

No hay nada que puede conseguir una base de datos de gráfico, que no se puede lograr mediante una base de datos relacional. Sin embargo, una base de datos de gráfico puede facilitar su express cierto tipo de consultas. Además, con optimizaciones específicas, pueden funcionar mejor determinadas consultas. Su decisión para elegir una u otra puede basarse en los siguientes factores:  
-   La aplicación tiene datos jerárquicos. El tipo de datos HierarchyID se puede usar para implementar las jerarquías, pero tiene algunas limitaciones. Por ejemplo, no permite almacenar varios elementos primarios de un nodo.
-   La aplicación tiene relaciones complejas de varios a varios; a medida que evoluciona la aplicación, se agregan nuevas relaciones.
-   Necesita analizar las relaciones y los datos interconectados.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Características del gráfico presentadas en [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Hemos empezado a agregar extensiones graph a SQL Server, para que sea más fácil almacenar y consultar datos del gráfico. Las características siguientes se presentan en la primera versión. 


### <a name="create-graph-objects"></a>Crear objetos de grafos
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] las extensiones le permitirá a los usuarios crear tablas de nodo o perimetral. Los nodos y bordes pueden tener propiedades asociadas a ellos. Puesto que los nodos y bordes se almacenan como tablas, se admiten todas las operaciones que se admiten en tablas relacionales en la tabla de nodo o perimetral. A continuación se muestra un ejemplo:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![tablas de amigos de persona](../../relational-databases/graphs/media/person-friends-tables.png "nodo Person y amigos perimetral tablas")  
Los nodos y bordes se almacenan como tablas  

### <a name="query-language-extensions"></a>Extensiones de lenguaje de consulta  
Nuevo `MATCH` cláusula se introdujo para admitir la coincidencia de patrones y navegación en saltos múltiples a través del gráfico. El `MATCH` función emplea la sintaxis de estilo de-arte ASCII para la coincidencia de patrones. Por ejemplo:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Completamente integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor 
Extensiones Graph están totalmente integradas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor. Usamos el mismo motor de almacenamiento, los metadatos, el procesador de consultas, etc. para almacenar y consultar datos del gráfico. Esto permite a los usuarios consultar a través de su gráfico y los datos relacionales en una sola consulta. Los usuarios también pueden beneficiarse de la combinación de las capacidades de graph con otros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologías como almacén de columnas, de alta disponibilidad, servicios de R, etcetera. Base de datos SQL graph también es compatible con todas la seguridad y cumplimiento de las características disponibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Las herramientas y el ecosistema  
Los usuarios se benefician de las herramientas existentes y el ecosistema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece. Herramientas como copia de seguridad y restauración, importación y exportación, funcionan sin problemas BCP desde el principio. Otras herramientas o servicios como SSIS, SSRS o Power BI funcionará con tablas de graph, simplemente la forma de trabajar con tablas relacionales.
 
 ## <a name="next-steps"></a>Pasos siguientes  
Leer el [gráfico SQL Database: arquitectura](./sql-graph-architecture.md)
   

