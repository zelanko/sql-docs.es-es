---
title: INDEXPROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- INDEXPROPERTY
- INDEXPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INDEXPROPERTY function
- indexes [SQL Server], viewing
- indexes [SQL Server], properties
ms.assetid: 998d5788-4871-44a8-8125-0d9390868b84
caps.latest.revision: 56
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cbd10b32ee6b2d88a97222c3a970452a4a628b83
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="indexproperty-transact-sql"></a>INDEXPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el valor de propiedad del índice con nombre o las estadísticas de un número de identificación, nombre de índice o estadísticas y nombre de propiedad de una tabla especificada. Devuelve NULL para los índices XML.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
INDEXPROPERTY ( object_ID , index_or_statistics_name , property )   
```  
  
## <a name="arguments"></a>Argumentos  
 *object_ID*  
 Es una expresión que contiene el número de identificación de objeto de la tabla o de la vista indizada de la que se va a proporcionar información de propiedades del índice. *object_ID* es **int**.  
  
 *index_or_statistics_name*  
 Es una expresión que contiene el nombre del índice o las estadísticas para los cuales se va a devolver la información de la propiedad. *index_or_statistics_name* es **nvarchar (128)**.  
  
 *propiedad*  
 Es una expresión que contiene el nombre de la propiedad de base de datos que se va a devolver. *propiedad* es **varchar (128)**, y puede tener uno de estos valores.  
  
> [!NOTE]  
>  A menos que se indique lo contrario, se devuelve NULL si *propiedad* no es un nombre de propiedad válido, *object_ID* no es un identificador de objeto válido, *object_ID* es un tipo de objeto no compatible la propiedad especificada o el autor de llamada no tiene permiso para ver los metadatos del objeto.  
  
|Propiedad|Description|Valor|  
|--------------|-----------------|-----------|  
|**IndexDepth**|Profundidad del índice.|Número de niveles del índice.<br /><br /> NULL = El índice o la entrada XML no es válido.|  
|**IndexFillFactor**|Valor de factor de relleno utilizado al crear o volver a generar el índice por última vez.|Factor de relleno|  
|**IndexID**|Id. del índice de una tabla o vista indizada especificada.|Id. del índice|  
|**IsAutoStatistics**|Las estadísticas han sido generadas por la opción AUTO_CREATE_STATISTICS de ALTER DATABASE.|1 = True<br /><br /> 0 = Falso o índice XML.|  
|**IsClustered**|El índice está agrupado.|1 = True<br /><br /> 0 = Falso o índice XML.|  
|**IsDisabled**|El índice está deshabilitado.|1 = True<br /><br /> 0 = False<br /><br /> NULL = La entrada no es válida.|  
|**IsFulltextKey**|El índice es la clave de indización semántica y de texto completo de una tabla.|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = Falso o índice XML.<br /><br /> NULL = La entrada no es válida.|  
|**IsHypothetical**|El índice es hipotético y no se puede utilizar directamente como ruta de acceso a datos. Los índices hipotéticos contienen estadísticas de nivel de columna y son conservados y utilizados por el Asistente para la optimización de motor de base de datos.|1 = True<br /><br /> 0 = Falso o índice XML<br /><br /> NULL = La entrada no es válida.|  
|**IsPadIndex**|El índice especifica el espacio que debe dejarse abierto en cada nodo interior.|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = Falso o índice XML.|  
|**IsPageLockDisallowed**|El valor de bloqueo de página establecido por la opción ALLOW_PAGE_LOCKS de ALTER INDEX.|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = No se permite el bloqueo de página.<br /><br /> 0 = Se permite el bloqueo de página.<br /><br /> NULL = La entrada no es válida.|  
|**IsRowLockDisallowed**|El valor de bloqueo de fila establecido por la opción ALLOW_ROW_LOCKS de ALTER INDEX.|**Se aplica a**: desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = No se permite el bloqueo de fila.<br /><br /> 0 = Se permite el bloqueo de fila.<br /><br /> NULL = La entrada no es válida.|  
|**IsStatistics**|*index_or_statistics_name* son las estadísticas creadas por la instrucción CREATE STATISTICS o por la opción AUTO_CREATE_STATISTICS de ALTER DATABASE.|1 = True<br /><br /> 0 = Falso o índice XML.|  
|**IsUnique**|El índice es exclusivo.|1 = True<br /><br /> 0 = Falso o índice XML.|  
|**IsColumnstore**|El índice es un índice de almacén de columnas optimizado de memoria xVelocity.|**Se aplica a**: desde [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].<br /><br /> 1 = True<br /><br /> 0 = False|  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="exceptions"></a>Excepciones  
 Devuelve NULL si se produce un error o si el autor de la llamada no tiene permiso para ver el objeto.  
  
 Un usuario solo puede ver los metadatos de elementos protegibles que posea o para los que se le haya concedido permiso. Esto significa que las funciones integradas de emisión de metadatos, como INDEXPROPERTY, pueden devolver NULL si el usuario no tiene ningún permiso para el objeto. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve los valores para la **IsClustered**, **IndexDepth**, y **IndexFillFactor** propiedades para la `PK`_`Employee` \_ `BusinessEntityID` índice de la `Employee` tabla el [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] base de datos.  
  
```  
SELECT   
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IsClustered')AS [Is Clustered],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexDepth') AS [Index Depth],  
    INDEXPROPERTY(OBJECT_ID('HumanResources.Employee'),  
        'PK_Employee_BusinessEntityID','IndexFillFactor') AS [Fill Factor];  
  
```  
  
 El conjunto de resultados es:  
  
```  
Is Clustered Index Depth Fill Factor   
------------ ----------- -----------   
1            2           0  
  
(1 row(s) affected)  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el ejemplo siguiente se examina las propiedades de uno de los índices en el `FactResellerSales` tabla.  
  
```  
-- Uses AdventureWorks  
  
SELECT   
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsClustered') AS [Is Clustered],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IsColumnstore') AS [Is Columnstore Index],  
INDEXPROPERTY(OBJECT_ID('dbo.FactResellerSales'),  
    'ClusteredIndex_6d10fa223e5e4c1fbba087e29e16a7a2','IndexFillFactor') AS [Fill Factor];  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [Estadísticas](../../relational-databases/statistics/statistics.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Sys.stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  


