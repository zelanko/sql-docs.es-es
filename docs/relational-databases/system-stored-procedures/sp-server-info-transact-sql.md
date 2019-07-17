---
title: sp_server_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_server_info
- sp_server_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_server_info
ms.assetid: 2dc2c262-3cfa-4a84-8127-3632ba583543
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6aae34fb03322a40f1b970df6271bb89d18b3293
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104451"
---
# <a name="spserverinfo-transact-sql"></a>sp_server_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista de nombres de atributos y sus valores correspondientes para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la puerta de enlace de la base de datos o el origen de datos subyacente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_server_info [[@attribute_id = ] 'attribute_id']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @attribute_id = ] 'attribute_id'` Es el identificador entero del atributo. *atributo* es **int**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**ATTRIBUTE_ID**|**int**|Número de Id. del atributo.|  
|**ATTRIBUTE_NAME**|**varchar (** 60 **)**|Nombre del atributo.|  
|**ATTRIBUTE_VALUE**|**varchar(** 255 **)**|Valor actual del atributo.|  
  
 En la tabla siguiente se enumeran los atributos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Bibliotecas de cliente ODBC utilizan actualmente los atributos **1**, **2**, **18**, **22**, y **500** en conexión tiempo.  
  
|ATTRIBUTE_ID|Descripción de ATTRIBUTE_NAME|ATTRIBUTE_VALUE|  
|-------------------|---------------------------------|----------------------|  
|**1**|DBMS_NAME|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**2**|DBMS_VER|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] - *x.xx.xxxx*|  
|**10**|OWNER_TERM|owner|  
|**11**|TABLE_TERM|table|  
|**12**|MAX_OWNER_NAME_LENGTH|128|  
|**13**|TABLE_LENGTH<br /><br /> Especifica el número máximo de caracteres de un nombre de tabla.|128|  
|**14**|MAX_QUAL_LENGTH<br /><br /> Especifica la longitud máxima del nombre de un calificador de tabla (la primera parte de un nombre de tabla de tres partes).|128|  
|**15**|COLUMN_LENGTH<br /><br /> Especifica el número máximo de caracteres de un nombre de columna.|128|  
|**16**|IDENTIFIER_CASE<br /><br /> Especifica los nombres definidos por el usuario (nombres de tablas, nombres de columnas, nombres de procedimientos almacenados) de la base de datos (el uso de mayúsculas y minúsculas en los objetos de los catálogos del sistema).|SENSITIVE|  
|**17**|TX_ISOLATION<br /><br /> Especifica el nivel de aislamiento de transacción inicial que da por supuesto el servidor, que corresponde a un nivel de aislamiento definido en SQL-92.|2|  
|**18**|COLLATION_SEQ<br /><br /> Especifica el orden del juego de caracteres para este servidor.|charset=iso_1 sort_order=dictionary_iso charset_num=1 sort_order_num=51|  
|**19**|SAVEPOINT_SUPPORT<br /><br /> Especifica si el DBMS subyacente admite puntos de retorno con nombre.|Y|  
|**20**|MULTI_RESULT_SETS<br /><br /> Especifica si la base de datos subyacente o la propia puerta de enlace admite varios conjuntos de resultados (si se pueden enviar a través de la puerta de enlace varias instrucciones que devuelvan varios conjuntos de resultados al cliente).|Y|  
|**22**|ACCESSIBLE_TABLES<br /><br /> Especifica si en **sp_tables**, la puerta de enlace devuelve solo las tablas, vistas y así sucesivamente, accesible por el usuario actual (es decir, el usuario que se seleccione al menos permisos para la tabla).|Y|  
|**100**|USERID_LENGTH<br /><br /> Especifica el número máximo de caracteres de un nombre de usuario.|128|  
|**101**|QUALIFIER_TERM<br /><br /> Especifica el término del proveedor de DBMS para un calificador de tabla (la primera parte de un nombre de tres partes).|database|  
|**102**|NAMED_TRANSACTIONS<br /><br /> Especifica si el DBMS subyacente acepta transacciones con nombre.|Y|  
|**103**|SPROC_AS_LANGUAGE<br /><br /> Especifica si los procedimientos almacenados se pueden ejecutar como eventos de lenguaje.|Y|  
|**104**|ACCESSIBLE_SPROC<br /><br /> Especifica si en **sp_stored_procedures**, la puerta de enlace solo devuelve procedimientos almacenados que son ejecutables por el usuario actual.|Y|  
|**105**|MAX_INDEX_COLS<br /><br /> Especifica el número máximo de columnas de un índice del DBMS.|16|  
|**106**|RENAME_TABLE<br /><br /> Especifica si se puede cambiar el nombre de las tablas.|Y|  
|**107**|RENAME_COLUMN<br /><br /> Especifica si se puede cambiar el nombre de las columnas.|Y|  
|**108**|DROP_COLUMN<br /><br /> Especifica si se pueden quitar columnas.|Y|  
|**109**|INCREASE_COLUMN_LENGTH<br /><br /> Especifica si se puede aumentar el tamaño de las columnas.|Y|  
|**110**|DDL_IN_TRANSACTION<br /><br /> Especifica si pueden aparecer instrucciones DDL en las transacciones.|Y|  
|**111**|DESCENDING_INDEXES<br /><br /> Especifica si se admiten índices descendentes.|Y|  
|**112**|SP_RENAME<br /><br /> Especifica si se puede cambiar el nombre de un procedimiento almacenado.|Y|  
|**113**|REMOTE_SPROC<br /><br /> Especifica si se pueden ejecutar procedimientos almacenados a través de las funciones de procedimientos almacenados remotos de DB-Library.|Y|  
|**500**|SYS_SPROC_VERSION<br /><br /> Especifica la versión de los procedimientos almacenados de catálogo actualmente implementados.|Número de versión actual|  
  
## <a name="remarks"></a>Comentarios  
 **sp_server_info** devuelve un subconjunto de la información proporcionada por **SQLGetInfo** en ODBC.  
  
## <a name="permissions"></a>Permisos  
 Es necesario contar con un permiso de tipo SELECT sobre el esquema.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
