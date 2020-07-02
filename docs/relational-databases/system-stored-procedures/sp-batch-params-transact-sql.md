---
title: sp_batch_params (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2b5c067b42d61c2dae1dbe247a6212611d155348
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716133"
---
# <a name="sp_batch_params-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Devuelve un conjunto de filas que contiene información sobre los parámetros incluidos en un [!INCLUDE[tsql](../../includes/tsql-md.md)] lote. **sp_batch_params** solo analiza el lote especificado y devuelve información acerca de los valores de los parámetros incrustados. No ejecuta el lote ni modifica el entorno de ejecución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tsqlbatch = ] 'tsqlbatch'`Es una cadena Unicode que contiene una [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción o lote para el que la información de parámetros se desea. *tsqlbatch* es de tipo **nvarchar (Max)** o implícitamente convertible a **nvarchar (Max)**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|Nombre del parámetro que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ha encontrado en el lote.|  
|**COLUMN_TYPE**|**smallint**|Este campo devuelve uno de los siguientes valores:<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> Esta columna siempre es 0.|  
|**DATA_TYPE**|**smallint**|Tipo de datos del parámetro (código entero para un tipo de datos ODBC). Si no se puede asignar este tipo de datos a un tipo de ISO, el valor es NULL. El nombre del tipo de datos nativo se devuelve en la columna **TYPE_NAME** . Este valor siempre es NULL.|  
|**TYPE_NAME**|**sysname**|Representación de cadena del tipo de datos como lo presenta el DBMS subyacente. Este valor es NULL.|  
|**PRECISIÓN**|**int**|Número de dígitos significativos. El valor devuelto para la columna **Precision** está en base 10.|  
|**LENGTH**|**int**|Tamaño de transferencia de los datos. Este valor es NULL.|  
|**ESCALA**|**smallint**|Número de dígitos a la derecha del separador decimal. Este valor es NULL.|  
|**FIJO**|**smallint**|Es la base de tipos numéricos. Este valor es NULL.|  
|**ACEPTA valores NULL**|**smallint**|Especifica la nulabilidad:<br /><br /> 1 = Tipo de datos de parámetro que se puede crear con valores NULL.<br /><br /> 0 = No se permiten valores NULL.<br /><br /> Este valor es NULL.|  
|**SQL_DATA_TYPE**|**smallint**|Valor del tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tal como aparece en el campo TYPE del descriptor. Esta columna es igual que la columna **data_type** , excepto los tipos de datos **DateTime** e **Interval** ISO. Esta columna siempre devuelve un valor. Este valor es NULL.|  
|**SQL_DATETIME_SUB**|**smallint**|El subcódigo de **intervalo** **DateTime** o ISO si el valor de **SQL_DATA_TYPE** es SQL_DATETIME o SQL_INTERVAL. Para tipos de datos distintos de **datetime** e **interval** de ISO, esta columna es NULL. Este valor es NULL.|  
|**CHAR_OCTET_LENGTH**|**int**|Longitud máxima en bytes de un parámetro de tipo de datos de **caracteres** o **binarios** . Para todos los demás tipos de datos, esta columna devuelve NULL. Este valor siempre es NULL.|  
|**ORDINAL_POSITION**|**int**|Posición ordinal del parámetro en el lote. Si el nombre del parámetro se repite varias veces, esta columna contiene el ordinal de la primera vez que aparece. El primer parámetro tiene el ordinal 1. Esta columna siempre devuelve un valor.|  
  
## <a name="permissions"></a>Permisos  
 El permiso para ejecutar **sp_batch_params** se concede a **Public**.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo muestra una consulta pasada a `sp_batch_params`. El conjunto de resultados enumera la lista de valores de parámetro incrustados.  
  
```  
DECLARE @SQLString nvarchar(500);  
/* Build the SQL string */  
SET @SQLString =  
     N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
     WHERE BusinessEntityID = @BusinessEntityID';  
EXECUTE sp_batch_params @SQLString;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Temas de procedimientos de ejecución de procedimientos almacenados &#40;ODBC&#41;](https://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [Ejecutar procedimientos almacenados &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
