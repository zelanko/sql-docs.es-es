---
title: Gráfico de procesamiento con SQL Server y Azure SQL Database | Microsoft Docs
ms.custom: ''
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
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb84f1cc40a05078910d10a48de67f1ac3467fe3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035901"
---
# <a name="graph-processing-with-sql-server-and-azure-sql-database"></a>Gráfico de procesamiento con SQL Server y Azure SQL Database
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece capacidades de base de datos de gráfico para modelar las relaciones de varios a varios. Las relaciones de graph se integran en [!INCLUDE[tsql-md](../../includes/tsql-md.md)] y recibir las ventajas de usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como el sistema de administración de base de datos fundamentales.


## <a name="what-is-a-graph-database"></a>¿Qué es una base de datos de gráfico?  
Una base de datos de gráficos es una colección de nodos (o vértices) y bordes (o relaciones). Un nodo representa una entidad (por ejemplo, una persona o una organización) y un borde representa una relación entre los dos nodos que conecta (por ejemplo, "Me gusta" o amigos). Los nodos y bordes pueden tener propiedades asociadas a ellos. Estas son algunas características que hacen que una base de datos de grafos sea única:  
-   Los bordes o las relaciones son entidades de primera clase en una base de datos de grafos y pueden tener atributos o propiedades asociados a ellas. 
-   Un solo borde puede conectar flexiblemente varios nodos en una base de datos de grafos.
-   Puede expresar fácilmente coincidencias de patrones y consultas de navegación en saltos múltiples.
-   Puede expresar fácilmente consultas polimórficas y cierres transitivos.

## <a name="when-to-use-a-graph-database"></a>Cuándo usar una base de datos de gráfico

No hay nada que una base de datos de grafos puede conseguir, que no se puede lograr mediante una base de datos relacional. Sin embargo, una base de datos de gráfico puede facilitar su express cierto tipo de consultas. Además, con optimizaciones específicas, pueden funcionar mejor determinadas consultas. La decisión para elegir una u otra puede basarse en los siguientes factores:  
-   La aplicación tiene datos jerárquicos. El tipo de datos HierarchyID se puede usar para implementar las jerarquías, pero tiene algunas limitaciones. Por ejemplo, no permite almacenar varios elementos primarios de un nodo.
-   La aplicación tiene relaciones complejas de varios a varios; a medida que evoluciona la aplicación, se agregan nuevas relaciones.
-   Necesita analizar las relaciones y los datos interconectados.

## <a name="graph-features-introduced-in-includesssqlv14includessssqlv14-mdmd"></a>Características del gráfico presentadas en [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] 
Hemos empezado a agregar extensiones graph a SQL Server, para que sea más fácil almacenar y consultar datos del gráfico. Las características siguientes se presentan en la primera versión. 


### <a name="create-graph-objects"></a>Crear objetos de grafos
[!INCLUDE[tsql-md](../../includes/tsql-md.md)] las extensiones le permitirá a los usuarios crear tablas de nodo o perimetral. Los nodos y bordes pueden tener propiedades asociadas a ellos. Puesto que los nodos y bordes se almacenan como tablas, se admiten todas las operaciones que se admiten en tablas relacionales en la tabla de nodo o perimetral. A continuación, se muestra un ejemplo:  

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
Extensiones Graph están totalmente integradas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor. Use el mismo motor de almacenamiento, los metadatos, el procesador de consultas, etc. para almacenar y consultar datos del gráfico. Consulta a través de graph y datos relacionales en una sola consulta. Combinación de funcionalidades de gráfico con otros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tecnologías como almacén de columnas, de alta disponibilidad, servicios de R, etcetera. Base de datos SQL graph también es compatible con todas la seguridad y cumplimiento de las características disponibles con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
 
### <a name="tooling-and-ecosystem"></a>Las herramientas y el ecosistema

Beneficiarse de las herramientas existentes y el ecosistema que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece. Herramientas como copia de seguridad y restauración, importación y exportación, funcionan sin problemas BCP desde el principio. Otras herramientas o servicios como SSIS, SSRS o Power BI funcionará con tablas de graph, simplemente la forma de trabajar con tablas relacionales.

## <a name="edge-constraints"></a>Restricciones perimetrales
Una restricción perimetral se define en una tabla de borde del gráfico y es un par de tablas de nodo que se puede conectar a un tipo de borde determinado. Esto ofrece a los usuarios un mejor control sobre su esquema de gráfico. Con la Ayuda de las restricciones perimetrales, los usuarios pueden restringir el tipo de nodos que se puede conectar un borde determinado. 

Para obtener información acerca de cómo crear y usar las restricciones perimetrales, consulte [las restricciones perimetrales](../../relational-databases/tables/graph-edge-constraints.md)

## <a name="merge-dml"></a>Mezcla de DML 
El [mezcla](../../t-sql/statements/merge-transact-sql.md) instrucción lleva a cabo Insertar, actualizar o eliminar operaciones en una tabla de destino basándose en los resultados de una combinación con una tabla de origen. Por ejemplo, puede sincronizar dos tablas insertando, actualizando o eliminando las filas de una tabla de destino basándose en las diferencias entre la tabla de destino y la tabla de origen. Ahora se admite el uso de predicados de coincidencia en una instrucción MERGE en Azure SQL Database y SQL Server vNext. Es decir, ahora es posible combinar los datos de gráfico actual (tablas de nodo o perimetral) con nuevos datos mediante los predicados de coincidencia para especificar relaciones de gráfico en una sola instrucción, en lugar de instrucciones INSERT, UPDATE o DELETE independientes.

Para obtener información acerca de cómo se puede usar la coincidencia de mezcla DML, consulte [instrucción MERGE](../../t-sql/statements/merge-transact-sql.md)

## <a name="shortest-path"></a>Ruta de acceso más corta
El [SHORTEST_PATH](./sql-graph-shortest-path.md) función busca la ruta más corta entre 2 nodos en un gráfico o a partir de un nodo determinado a todos los nodos en el gráfico. También puede utilizarse para buscar un cierre transitivo ruta más corta o para los recorridos de longitud arbitraria en el gráfico. 

 ## <a name="next-steps"></a>Pasos siguientes  
Leer el [gráfico SQL Database: arquitectura](./sql-graph-architecture.md)
   

