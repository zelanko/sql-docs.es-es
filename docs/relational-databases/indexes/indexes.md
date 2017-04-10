---
title: "&#205;ndices | Microsoft Docs"
ms.custom: ""
ms.date: "11/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "tipos de índice [SQL Server]"
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# &#205;ndices
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En la tabla siguiente se indican los tipos de índice disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se proporcionan vínculos a información adicional.  
  
|Tipo de índice|Descripción|Información adicional|  
|----------------|-----------------|----------------------------|  
|Hash|Con un índice hash, se accede a los datos a través de una tabla hash en memoria. Los índices hash utilizan una cantidad fija de memoria, que es una función del número de depósitos.|[Directrices para usar índices en las tablas con optimización para memoria](../Topic/Guidelines%20for%20Using%20Indexes%20on%20Memory-Optimized%20Tables.md)|  
|Índices no clúster con optimización para memoria|Para los índices no clúster con optimización para memoria, el consumo de memoria depende del número de filas y del tamaño de las columnas de clave de índice.|[Directrices para usar índices en las tablas con optimización para memoria](../Topic/Guidelines%20for%20Using%20Indexes%20on%20Memory-Optimized%20Tables.md)|  
|Clúster|Un índice clúster ordena y almacena las filas de datos de la tabla o vista por orden en función de la clave del índice clúster. El índice clúster se implementa como una estructura de árbol b que admite la recuperación rápida de las filas a partir de los valores de las claves del índice clúster.|[Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Crear índices clúster](../../relational-databases/indexes/create-clustered-indexes.md)|  
|No agrupado|Los índices no clúster se pueden definir en una tabla o vista con un índice clúster o en un montón. Cada fila del índice no clúster contiene un valor de clave no agrupada y un localizador de fila. Este localizador apunta a la fila de datos del índice clúster o el montón que contiene el valor de clave. Las filas del índice se almacenan en el mismo orden que los valores de la clave del índice, pero no se garantiza que las filas de datos estén en un determinado orden a menos que se cree un índice clúster en la tabla.|[Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)<br /><br /> [Crear índices no clúster](../../relational-databases/indexes/create-nonclustered-indexes.md)|  
|Único|Un índice único se asegura de que la clave de índice no contenga valores duplicados y, por tanto, cada fila de la tabla o vista sea en cierta forma única.<br /><br /> La unicidad puede ser una propiedad tanto de índices clúster como de índices no clúster.|[Crear índices únicos](../../relational-databases/indexes/create-unique-indexes.md)|  
|Almacén de columnas|El índice de almacén de columnas en memoria almacena y administra los datos mediante el almacenamiento de datos basado en columnas y el procesamiento de consultas basado en columnas.<br /><br /> Los índices de almacén de columnas funcionan correctamente para las cargas de trabajo de almacenamiento de datos que ejecutan principalmente cargas masivas y consultas de solo lectura. Use el índice de almacén de columnas para aumentar **hasta en diez veces el rendimiento de las consultas** en relación con el almacenamiento tradicional orientado a filas, y hasta **en siete veces la compresión de datos** en relación con el tamaño de los datos sin comprimir.|[Guía de índices de almacén de columnas](../Topic/Columnstore%20Indexes%20Guide.md)<br /><br /> [Usar índices no clúster de almacén de columnas](https://msdn.microsoft.com/en-us/library/dn589806.aspx)|  
|Índice con columnas incluidas|Índice no clúster que se extiende para incluir columnas sin clave además de las columnas de clave.|[Crear índices con columnas incluidas](../../relational-databases/indexes/create-indexes-with-included-columns.md)|  
|Índice en columnas calculadas|Índice de una columna que se deriva del valor de una o varias columnas, o algunas entradas deterministas.|[Índices en columnas calculadas](../../relational-databases/indexes/indexes-on-computed-columns.md)|  
|Filtrado|Índice no clúster optimizado, especialmente indicado para cubrir consultas que seleccionan de un subconjunto bien definido de datos. Utiliza un predicado de filtro para indizar una parte de las filas de la tabla. Un índice filtrado bien diseñado puede mejorar el rendimiento de las consultas y reducir los costos de almacenamiento del índice en relación con los índices de tabla completa, así como los costos de mantenimiento.|[Crear índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md)|  
|Espacial|Un índice espacial permite realizar de forma más eficaz determinadas operaciones en objetos espaciales (*datos espaciales*) en una columna del tipo de datos de **geometry**. El índice espacial reduce el número de objetos a los que es necesario aplicar las operaciones espaciales, que son relativamente costosas.|[Información general sobre los índices espaciales](../../relational-databases/spatial/spatial-indexes-overview.md)|  
|XML|Representación dividida y persistente de los objetos binarios grandes (BLOB) XML de la columna de tipo de datos **xml**.|[Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)|  
|Texto completo|Tipo especial de índice funcional basado en símbolos (token) que compila y mantiene el motor de texto completo de Microsoft para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Proporciona la compatibilidad adecuada para búsquedas de texto complejas en datos de cadenas de caracteres.|[Rellenar índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md)|  
  
## Tareas relacionadas  
  
## Contenido relacionado  
 [Opción SORT_IN_TEMPDB para índices](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)  
  
 [Deshabilitar índices y restricciones](../../relational-databases/indexes/disable-indexes-and-constraints.md)  
  
 [Habilitar índices y restricciones](../../relational-databases/indexes/enable-indexes-and-constraints.md)  
  
 [Cambiar el nombre a los índices](../../relational-databases/indexes/rename-indexes.md)  
  
 [Establecer opciones de índice](../../relational-databases/indexes/set-index-options.md)  
  
 [Requisitos de espacio en disco para operaciones DDL de índice](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
 [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
 [Especificar el factor de relleno para un índice](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)  
  
## Vea también  
 [Índices agrupados y no agrupados descritos](../../relational-databases/indexes/clustered-and-nonclustered-indexes-described.md)  
  
  