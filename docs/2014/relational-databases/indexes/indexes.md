---
title: Índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index types [SQL Server]
ms.assetid: 00863b10-e77c-44c5-8ac2-bb4ac454eec6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 58d4d71189598a6fd101e6db0a40b8c8b0a3b903
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161852"
---
# <a name="indexes"></a>Índices
  En la tabla siguiente se indican los tipos de índice disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se proporcionan vínculos a información adicional.  
  
|Tipo de índice|Descripción|Información adicional|  
|----------------|-----------------|----------------------------|  
|Hash|Con un índice hash, se accede a los datos a través de una tabla hash en memoria. Los índices hash utilizan una cantidad fija de memoria, que es una función del número de cubos.|[Directrices para usar índices en las tablas con optimización para memoria](../in-memory-oltp/memory-optimized-tables.md)|  
|Índices no clúster optimizados para memoria|Para los índices no clúster optimizados para memoria, el consumo de memoria depende del número de filas y del tamaño de las columnas de clave de índice.|[Directrices para usar índices en las tablas con optimización para memoria](../in-memory-oltp/memory-optimized-tables.md)|  
|Clúster|Un índice clúster ordena y almacena las filas de datos de la tabla o vista por orden en función de la clave del índice clúster. El índice clúster se implementa como una estructura de árbol b que admite la recuperación rápida de las filas a partir de los valores de las claves del índice clúster.|[Índices agrupados y no agrupados descritos](clustered-and-nonclustered-indexes-described.md)<br /><br /> [Crear índices clúster](create-clustered-indexes.md)|  
|No agrupado|Los índices no clúster se pueden definir en una tabla o vista con un índice clúster o en un montón. Cada fila del índice no clúster contiene un valor de clave no agrupada y un localizador de fila. Este localizador apunta a la fila de datos del índice clúster o el montón que contiene el valor de clave. Las filas del índice se almacenan en el mismo orden que los valores de la clave del índice, pero no se garantiza que las filas de datos estén en un determinado orden a menos que se cree un índice clúster en la tabla.|[Índices agrupados y no agrupados descritos](clustered-and-nonclustered-indexes-described.md)<br /><br /> [Crear índices no clúster](create-nonclustered-indexes.md)|  
|Único|Un índice único se asegura de que la clave de índice no contenga valores duplicados y, por tanto, cada fila de la tabla o vista sea en cierta forma única.<br /><br /> La unicidad puede ser una propiedad tanto de índices clúster como de índices no clúster.|[Crear índices únicos](create-unique-indexes.md)|  
|columnstore|El índice de almacén de columnas en memoria almacena y administra los datos mediante el almacenamiento de datos basado en columnas y el procesamiento de consultas basado en columnas.<br /><br /> Los índices de almacén de columnas funcionan correctamente para las cargas de trabajo de almacenamiento de datos que ejecutan principalmente cargas masivas y consultas de solo lectura. Use el índice de almacén de columnas para aumentar **hasta en diez veces el rendimiento de las consultas** en relación con el almacenamiento tradicional orientado a filas, y hasta **en siete veces la compresión de datos** en relación con el tamaño de los datos sin comprimir.|[Descripción de los índices de almacén de columnas](columnstore-indexes-described.md)<br /><br /> [Usar índices no agrupados de almacén de columnas](../../database-engine/using-nonclustered-columnstore-indexes.md)<br /><br /> [El uso de índices de almacén de columnas agrupado](../../database-engine/using-clustered-columnstore-indexes.md)|  
|Índice con columnas incluidas|Índice no clúster que se extiende para incluir columnas sin clave además de las columnas de clave.|[Crear índices con columnas incluidas](create-indexes-with-included-columns.md)|  
|Índice en columnas calculadas|Índice de una columna que se deriva del valor de una o varias columnas, o algunas entradas deterministas.|[Índices en columnas calculadas](indexes-on-computed-columns.md)|  
|Filtrado|Índice no clúster optimizado, especialmente indicado para cubrir consultas que seleccionan de un subconjunto bien definido de datos. Utiliza un predicado de filtro para indizar una parte de las filas de la tabla. Un índice filtrado bien diseñado puede mejorar el rendimiento de las consultas y reducir los costos de almacenamiento del índice en relación con los índices de tabla completa, así como los costos de mantenimiento.|[Crear índices filtrados](create-filtered-indexes.md)|  
|Espacial|Un índice espacial permite realizar de forma más eficaz determinadas operaciones en objetos espaciales (*datos espaciales*) en una columna del tipo de datos de **geometry** . El índice espacial reduce el número de objetos a los que es necesario aplicar las operaciones espaciales, que son relativamente costosas.|[Información general sobre los índices espaciales](../spatial/spatial-indexes-overview.md)|  
|XML|Representación dividida y persistente de los objetos binarios grandes (BLOB) XML de la columna de tipo de datos `xml`.|[Índices XML &#40;SQL Server&#41;](../xml/xml-indexes-sql-server.md)|  
|Texto completo|Tipo especial de índice funcional basado en símbolos (token) que compila y mantiene el motor de texto completo de Microsoft para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Proporciona la compatibilidad adecuada para búsquedas de texto complejas en datos de cadenas de caracteres.|[Rellenar índices de texto completo](../search/populate-full-text-indexes.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
## <a name="related-content"></a>Contenido relacionado  
 [Opción SORT_IN_TEMPDB para índices](sort-in-tempdb-option-for-indexes.md)  
  
 [Deshabilitar índices y restricciones](disable-indexes-and-constraints.md)  
  
 [Habilitar índices y restricciones](enable-indexes-and-constraints.md)  
  
 [Cambiar el nombre de los índices](rename-indexes.md)  
  
 [Establecer opciones de índice](set-index-options.md)  
  
 [Requisitos de espacio en disco para operaciones DDL de índice](disk-space-requirements-for-index-ddl-operations.md)  
  
 [Reorganizar y volver a generar índices](reorganize-and-rebuild-indexes.md)  
  
 [Especificar el factor de relleno para un índice](specify-fill-factor-for-an-index.md)  
  
## <a name="see-also"></a>Vea también  
 [Índices agrupados y no agrupados descritos](clustered-and-nonclustered-indexes-described.md)  
  
  
