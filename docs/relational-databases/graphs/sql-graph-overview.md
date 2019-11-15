---
title: Procesamiento de gráficos
titleSuffix: SQL Server and Azure SQL Database
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, overview
ms.assetid: ''
author: shkale-msft
ms.author: shkale
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3ca26af4738de25937b71e0c97c6272414a0957a
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096086"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Procesamiento de gráficos con SQL Server y Azure SQL Database
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece capacidades de base de datos de gráficos para modelar las relaciones varios a varios. Las relaciones de gráficos se integran en [!INCLUDE[tsql-md](../../includes/tsql-md.md)] y reciben las ventajas de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como sistema de administración de bases de datos base.


## <a name="what-is-a-graph-database"></a>¿Qué es una base de datos de grafos?  
Una base de datos de gráficos es una colección de nodos (o vértices) y bordes (o relaciones). Un nodo representa una entidad (por ejemplo, una persona o una organización) y un borde representa una relación entre los dos nodos que conecta (por ejemplo, gustos o amigos). Tanto los nodos como los bordes pueden tener propiedades asociadas. Estas son algunas de las características que hacen que una base de datos de grafos sea única:  
-   Los bordes o las relaciones son entidades de primera clase en una base de datos de gráficos y pueden tener atributos o propiedades asociados. 
-   Un solo borde puede conectar de forma flexible varios nodos en una base de datos de grafos.
-   Puede expresar fácilmente la coincidencia de patrones y las consultas de navegación de varios saltos.
-   Puede expresar fácilmente consultas de cierre transitivo y polimórficos.

## <a name="when-to-use-a-graph-database"></a>Cuándo usar una base de datos de grafos

No hay nada que pueda conseguir una base de datos de gráficos, lo que no se puede lograr mediante una base de datos relacional. Sin embargo, una base de datos de gráficos puede facilitar la rápida expresión de determinados tipos de consultas. Además, con optimizaciones específicas, algunas consultas pueden funcionar mejor. La decisión de elegir una sobre la otra puede basarse en los siguientes factores:  
-   La aplicación tiene datos jerárquicos. El tipo de texto HierarchyID se puede usar para implementar jerarquías, pero tiene algunas limitaciones. Por ejemplo, no permite almacenar varios elementos primarios para un nodo.
-   La aplicación tiene relaciones de varios a varios complejas; a medida que la aplicación evoluciona, se agregan nuevas relaciones.
-   Debe analizar los datos y las relaciones interconectadas.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Características de gráficos introducidas en [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Vamos a empezar a agregar extensiones de grafos a SQL Server para facilitar el almacenamiento y la consulta de datos de gráfico. Las siguientes características se incluyen en la primera versión. 


### <a name="create-graph-objects"></a>Crear objetos de gráfico
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] extensiones permitirán a los usuarios crear tablas de nodos o perimetrales. Tanto los nodos como los bordes pueden tener propiedades asociadas. Dado que los nodos y los bordes se almacenan como tablas, todas las operaciones que se admiten en las tablas relacionales se admiten en el nodo o la tabla perimetral. A continuación se muestra un ejemplo:  

```   
CREATE TABLE Person (ID INTEGER PRIMARY KEY, Name VARCHAR(100), Age INT) AS NODE;
CREATE TABLE friends (StartDate date) AS EDGE;
```   

![persona-Friends-tablas](../../relational-databases/graphs/media/person-friends-tables.png "Tablas de los límites de amigos y nodos de personas")  
Los nodos y los bordes se almacenan como tablas  

### <a name="query-language-extensions"></a>Extensiones de lenguaje de consulta  
La nueva cláusula `MATCH` se incluye para admitir la búsqueda de coincidencias de patrones y la navegación de varios saltos a través del gráfico. La función `MATCH` utiliza la sintaxis de estilo ASCII-Art para la coincidencia de patrones. Por ejemplo:  

```   
-- Find friends of John
SELECT Person2.Name 
FROM Person Person1, Friends, Person Person2
WHERE MATCH(Person1-(Friends)->Person2)
AND Person1.Name = 'John';
```   
 
### <a name="fully-integrated-in-includessnoversionincludesssnoversion-mdmd-engine"></a>Totalmente integrado en el motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 
Las extensiones de grafos están totalmente integradas en el motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use el mismo motor de almacenamiento, metadatos, procesador de consultas, etc. para almacenar y consultar los datos del gráfico. Realizar consultas en los datos de gráfico y relacionales en una sola consulta. Combinación de funcionalidades de gráficos con otras tecnologías de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como almacén de columnas, HA, R Services, etc. La base de datos de SQL Graph también es compatible con todas las características de seguridad y cumplimiento disponibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Herramientas y ecosistema

Benefíciese de las herramientas y el ecosistema existentes que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece. Herramientas como la copia de seguridad y la restauración, la importación y la exportación, BCP funciona fuera de la caja. Otras herramientas o servicios como SSIS, SSRS o Power BI funcionarán con las tablas de gráficos, de la misma forma en que trabajan con tablas relacionales.

## <a name="edge-constraints"></a>Restricciones perimetrales
Se define una restricción perimetral en una tabla irregular del gráfico y es un par de tablas de nodos a las que puede conectarse un tipo de borde determinado. Esto proporciona a los usuarios un mejor control sobre el esquema del grafo. Con la ayuda de las restricciones perimetrales, los usuarios pueden restringir el tipo de nodos a los que se puede conectar un borde determinado. 

Para obtener más información sobre cómo crear y usar restricciones perimetrales, consulte [restricciones perimetrales](../../relational-databases/tables/graph-edge-constraints.md) .

## <a name="merge-dml"></a>Combinar DML 
La instrucción [Merge](../../t-sql/statements/merge-transact-sql.md) realiza operaciones de inserción, actualización o eliminación en una tabla de destino en función de los resultados de una combinación con una tabla de origen. Por ejemplo, puede sincronizar dos tablas insertando, actualizando o eliminando filas en una tabla de destino en función de las diferencias entre la tabla de destino y la tabla de origen. Ahora se admite el uso de predicados MATCH en una instrucción MERGE en Azure SQL Database y SQL Server vNext. Es decir, ahora es posible fusionar mediante combinación los datos actuales del grafo (tablas de nodo o perimetrales) con nuevos datos mediante los predicados de coincidencia para especificar las relaciones de los gráficos en una sola instrucción, en lugar de las instrucciones INSERT/UPDATE/DELETE independientes.

Para obtener más información sobre cómo se puede usar la coincidencia en Merge DML, consulte [instrucción Merge](../../t-sql/statements/merge-transact-sql.md) .

## <a name="shortest-path"></a>Ruta más corta
La función [SHORTEST_PATH](./sql-graph-shortest-path.md) encuentra la ruta más corta entre los dos nodos de un gráfico o el inicio de un nodo determinado a todos los demás nodos del gráfico. La ruta de acceso más corta también se puede usar para buscar un cierre transitivo o para recorridos de longitud arbitrarios en el gráfico. 

 ## <a name="next-steps"></a>Pasos siguientes  
Leer la [arquitectura de base de datos de SQL Graph](./sql-graph-architecture.md)
   

