---
title: sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9872a4debd79b36015844baee7bb84a3d570d8b8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spestimatedrowsizereductionforvardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Calcula la reducción del tamaño medio de las filas si se habilita el formato de almacenamiento vardecimal en una tabla. Utilice este número para calcular la reducción general del tamaño de la tabla. Puesto que el muestreo estadístico se usa para calcular la reducción media del tamaño de fila, se debe considerar como una mera aproximación. Es posible que, en contadas ocasiones, el tamaño de fila aumente después de habilitar el formato de almacenamiento vardecimal.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, use el tipo de compresión ROW y PAGE. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md). Para los efectos de la compresión en el tamaño de tablas e índices, vea [sp_estimate_data_compression_savings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@table=** ] **'***tabla***'**  
 Es el nombre de tres partes de la tabla para la que se debe cambiar el formato de almacenamiento. *tabla* es **nvarchar(776)**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 El siguiente conjunto de resultados se devuelve para proporcionar información acerca del tamaño de tabla actual y aproximado.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**decimal (12, 2)**|Representa la longitud de la fila en formato de almacenamiento decimal fijo.|  
|**avg_rowlen_vardecimal_format**|**decimal (12, 2)**|Representa el tamaño de fila medio cuando se utiliza el formato de almacenamiento vardecimal.|  
|**row_count**|**int**|Número de filas de la tabla.|  
  
## <a name="remarks"></a>Comentarios  
 Use **sp_estimated_rowsize_reduction_for_vardecimal** para calcular el ahorro que son el resultado si habilita una tabla para el formato de almacenamiento vardecimal. Por ejemplo, si el tamaño medio de una fila se puede reducir un 40 por ciento, potencialmente también se puede reducir el tamaño de la tabla en un 40 por ciento. Es posible que no consiga ahorrar espacio, ya que dependerá del factor de relleno y del tamaño de la fila. Por ejemplo, si una fila tiene 8.000 bytes de longitud y reduce su tamaño en un 40 por ciento, solo podrá seguir incluyendo una fila en una página de datos, con lo que no obtendrá ningún ahorro.  
  
 Si los resultados de **sp_estimated_rowsize_reduction_for_vardecimal** indican que la tabla crecerá, eso quiere decir que muchas filas de la tabla utilizan prácticamente toda la precisión de los tipos de datos decimal y la adición de la pequeña sobrecarga necesaria para el formato de almacenamiento vardecimal es mayor que el ahorro del formato de almacenamiento vardecimal. En este caso excepcional, no habilite el formato de almacenamiento vardecimal.  
  
 Si una tabla está habilitada para el formato de almacenamiento vardecimal, use **sp_estimated_rowsize_reduction_for_vardecimal** para estimar el tamaño promedio de la fila si se deshabilita el formato de almacenamiento vardecimal.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso CONTROL en la tabla.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente calcula la reducción del tamaño de fila si se comprime la tabla `Production.WorkOrderRouting` de la base de datos `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_db_vardecimal_storage_format &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
