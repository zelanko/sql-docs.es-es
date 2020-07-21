---
title: Índices | Microsoft Docs
ms.custom: ''
ms.date: 12/21/2016
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e980013658fd83c4f8c934e6e8b2b51d27783893
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760769"
---
# <a name="indexes"></a>Índices
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

## <a name="available-index-types"></a>Tipos de índices disponibles
En la tabla siguiente se indican los tipos de índice disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se proporcionan vínculos a información adicional.  
  
|Tipo de índice|Descripción|Información adicional|  
|----------------|-----------------|----------------------------|  
|Hash|Con un índice hash, se accede a los datos a través de una tabla hash en memoria. Los índices hash utilizan una cantidad fija de memoria, que es una función del número de cubos.|[Directrices para usar índices en las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [Directrices para diseñar índices de hash](../../relational-databases/sql-server-index-design-guide.md#hash_index)|  
|Índice no agrupado optimizado para memoria|Para los índices no clúster optimizados para memoria, el consumo de memoria depende del número de filas y del tamaño de las columnas de clave de índice.|[Directrices para usar índices en las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)<br /><br /> [Directrices para diseñar índices no agrupados optimizados para memoria](../../relational-databases/sql-server-index-design-guide.md#inmem_nonclustered_index)|  
|Clúster|Un índice clúster ordena y almacena las filas de datos de la tabla o vista por orden en función de la clave del índice clúster. El índice clúster se implementa como una estructura de árbol b que admite la recuperación rápida de las filas a partir de los valores de las claves del índice clúster.|[Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)<br /><br /> [Directrices para diseñar índices agrupados](../../relational-databases/sql-server-index-design-guide.md#Clustered)|  
|No agrupado|Los índices no clúster se pueden definir en una tabla o vista con un índice clúster o en un montón. Cada fila del índice no clúster contiene un valor de clave no agrupada y un localizador de fila. Este localizador apunta a la fila de datos del índice clúster o el montón que contiene el valor de clave. Las filas del índice se almacenan en el mismo orden que los valores de la clave del índice, pero no se garantiza que las filas de datos estén en un determinado orden a menos que se cree un índice clúster en la tabla.|[Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)<br /><br /> [Directrices para diseñar índices no agrupados](../../relational-databases/sql-server-index-design-guide.md#Nonclustered)|  
|Único|Un índice único se asegura de que la clave de índice no contenga valores duplicados y, por tanto, cada fila de la tabla o vista sea en cierta forma única.<br /><br /> La unicidad puede ser una propiedad tanto de índices clúster como de índices no clúster.|[Crear índices únicos](../../relational-databases/indexes/create-unique-indexes.md)<br /><br /> [Directrices para diseñar índices únicos](../../relational-databases/sql-server-index-design-guide.md#Unique)|  
|columnstore|El índice de almacén de columnas en memoria almacena y administra los datos mediante el almacenamiento de datos basado en columnas y el procesamiento de consultas basado en columnas.<br /><br /> Los índices de almacén de columnas funcionan correctamente para las cargas de trabajo de almacenamiento de datos que ejecutan principalmente cargas masivas y consultas de solo lectura. Use el índice de almacén de columnas para aumentar **hasta en diez veces el rendimiento de las consultas** en relación con el almacenamiento tradicional orientado a filas, y hasta **en siete veces la compresión de datos** en relación con el tamaño de los datos sin comprimir.|[Descripción de los índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md)<br /><br /> [Directrices para diseñar índices de almacén de columnas](../../relational-databases/sql-server-index-design-guide.md#columnstore_index)|  
|Índice con columnas incluidas|Índice no clúster que se extiende para incluir columnas sin clave además de las columnas de clave.|[Crear índices con columnas incluidas](../../relational-databases/indexes/create-indexes-with-included-columns.md)|  
|Índice en columnas calculadas|Índice de una columna que se deriva del valor de una o varias columnas, o algunas entradas deterministas.|[Índices en columnas calculadas](../../relational-databases/indexes/indexes-on-computed-columns.md)|  
|Filtered|Índice no clúster optimizado, especialmente indicado para cubrir consultas que seleccionan de un subconjunto bien definido de datos. Utiliza un predicado de filtro para indizar una parte de las filas de la tabla. Un índice filtrado bien diseñado puede mejorar el rendimiento de las consultas y reducir los costos de almacenamiento del índice en relación con los índices de tabla completa, así como los costos de mantenimiento.|[Crear índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md)<br /><br /> [Directrices para diseñar índices filtrados](../../relational-databases/sql-server-index-design-guide.md#Filtered)|  
|Espacial|Un índice espacial permite realizar de forma más eficaz determinadas operaciones en objetos espaciales (*datos espaciales*) en una columna del tipo de datos de **geometry** . El índice espacial reduce el número de objetos a los que es necesario aplicar las operaciones espaciales, que son relativamente costosas.|[Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)|  
|XML|Representación dividida y persistente de los objetos binarios grandes (BLOB) XML de la columna de tipo de datos **xml**.|[Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)|  
|Texto completo|Tipo especial de índice funcional basado en símbolos (token) que compila y mantiene el motor de texto completo de Microsoft para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Proporciona la compatibilidad adecuada para búsquedas de texto complejas en datos de cadenas de caracteres.|[Rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)|  
  
## <a name="related-content"></a>Contenido relacionado  
 [Guía de diseño de índices de SQL Server](../../relational-databases/sql-server-index-design-guide.md)      
 [Opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)     
 [Deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md)     
 [Habilitar índices y restricciones](../../relational-databases/indexes/enable-indexes-and-constraints.md)    
 [Cambiar el nombre de los índices](../../relational-databases/indexes/rename-indexes.md)     
 [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md)     
 [Requisitos de espacio en disco para operaciones DDL de índice](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)     
 [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)     
 [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)     
 [Guía de arquitectura de páginas y extensiones](../../relational-databases/pages-and-extents-architecture-guide.md)     
 [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)     
  
