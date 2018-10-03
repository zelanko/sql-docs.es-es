---
title: sp_fkeys (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fkeys
- sp_fkeys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fkeys
ms.assetid: 18110444-d38d-4cff-90d2-d1fc6236668b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a30016240c6cfd34cd2e21d6987ea04a0bc27537
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705973"
---
# <a name="spfkeys-transact-sql"></a>sp_fkeys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve información acerca de las claves externas lógicas del entorno actual. Este procedimiento muestra las relaciones de las claves externas, incluidas las claves externas deshabilitadas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_fkeys [ @pktable_name = ] 'pktable_name'   
     [ , [ @pktable_owner = ] 'pktable_owner' ]   
     [ , [ @pktable_qualifier = ] 'pktable_qualifier' ]   
     { , [ @fktable_name = ] 'fktable_name' }   
     [ , [ @fktable_owner = ] 'fktable_owner' ]   
     [ , [ @fktable_qualifier = ] 'fktable_qualifier' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @pktable_name=] '*pktable_name*'  
 Es el nombre de la tabla, con la clave externa, utilizada para devolver información del catálogo. *pktable_name* es **sysname**, su valor predeterminado es null. No se admite la coincidencia de patrón de caracteres comodín. Este parámetro o el *fktable_name* parámetro, o ambos, deben proporcionarse.  
  
 [ @pktable_owner=] '*pktable_owner*'  
 Es el nombre del propietario de la tabla (con la clave principal) se usa para devolver información del catálogo. *pktable_owner* es **sysname**, su valor predeterminado es null. No se admite la coincidencia de patrón de caracteres comodín. Si *pktable_owner* no se especifica, se aplican las reglas predeterminadas de visibilidad de tabla del DBMS subyacente.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el usuario actual es propietario de una tabla con el nombre especificado, se devuelven las columnas de esa tabla. Si *pktable_owner* no se especifica y el usuario actual no posee una tabla con los valores especificados *pktable_name*, el procedimiento busca una tabla con los valores especificados *pktable_name* que pertenezca al propietario de la base de datos. Si hay una, se devuelven las columnas de esa tabla.  
  
 [ @pktable_qualifier =] '*pktable_qualifier*'  
 Es el nombre del calificador de la tabla (con la clave principal). *pktable_qualifier* es de tipo sysname y su valor predeterminado es NULL. Varios productos DBMS admiten nombres de tres partes para tablas (*qualifier.owner.name*). En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el calificador representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla.  
  
 [ @fktable_name=] '*fktable_name*'  
 Es el nombre de la tabla, con una clave externa, utilizada para devolver información del catálogo. *fktable_name* es de tipo sysname y su valor predeterminado es NULL. No se admite la coincidencia de patrón de caracteres comodín. Este parámetro o el *pktable_name* parámetro, o ambos, deben proporcionarse.  
  
 [ @fktable_owner =] '*fktable_owner*'  
 Es el nombre del propietario de la tabla, con una clave externa, utilizada para devolver información del catálogo. *fktable_owner* es **sysname**, su valor predeterminado es null. No se admite la coincidencia de patrón de caracteres comodín. Si *fktable_owner* no se especifica, se aplican las reglas predeterminadas de visibilidad de tabla del DBMS subyacente.  
  
 En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el usuario actual es propietario de una tabla con el nombre especificado, se devuelven las columnas de esa tabla. Si *fktable_owner* no se especifica y el usuario actual no posee una tabla con los valores especificados *fktable_name*, el procedimiento busca una tabla con los valores especificados *fktable_name* que pertenezca al propietario de la base de datos. Si hay una, se devuelven las columnas de esa tabla.  
  
 [ @fktable_qualifier=] '*fktable_qualifier*'  
 Es el nombre del calificador de la tabla (con una clave externa). *fktable_qualifier* es **sysname**, su valor predeterminado es null. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el calificador representa el nombre de la base de datos. En algunos productos, representa el nombre del servidor del entorno de base de datos de la tabla.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|PKTABLE_QUALIFIER|**sysname**|Nombre del calificador de la tabla (con la clave principal). Este campo puede ser NULL.|  
|PKTABLE_OWNER|**sysname**|Nombre del propietario de la tabla (con la clave principal). Este campo siempre devuelve un valor.|  
|PKTABLE_NAME|**sysname**|Nombre de la tabla (con la clave principal). Este campo siempre devuelve un valor.|  
|PKCOLUMN_NAME|**sysname**|Nombre de las columnas de clave principal para cada columna de TABLE_NAME devuelta. Este campo siempre devuelve un valor.|  
|FKTABLE_QUALIFIER|**sysname**|Nombre del calificador de la tabla (con una clave externa). Este campo puede ser NULL.|  
|FKTABLE_OWNER|**sysname**|Nombre del propietario de la tabla (con una clave externa). Este campo siempre devuelve un valor.|  
|FKTABLE_NAME|**sysname**|Nombre de la tabla (con una clave externa). Este campo siempre devuelve un valor.|  
|FKCOLUMN_NAME|**sysname**|Nombre de la columna de clave externa para cada columna de TABLE_NAME devuelta. Este campo siempre devuelve un valor.|  
|KEY_SEQ|**smallint**|Número de secuencia de la columna en una clave principal con varias columnas. Este campo siempre devuelve un valor.|  
|UPDATE_RULE|**smallint**|Acción aplicada a la clave externa si la operación de SQL es una actualización.  Valores posibles:<br /> 0=CASCADE cambia a clave externa.<br /> 1=NO ACTION cambia si la clave externa está presente.<br />   2 = establecer como null <br /> 3 = Establecer valor predeterminado |  
|DELETE_RULE|**smallint**|Acción aplicada a la clave externa si la operación de SQL es una eliminación. Valores posibles:<br /> 0=CASCADE cambia a clave externa.<br /> 1=NO ACTION cambia si la clave externa está presente.<br />   2 = establecer como null <br /> 3 = Establecer valor predeterminado |  
|FK_NAME|**sysname**|Identificador de la clave externa. Es NULL si no es aplicable al origen de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve el nombre de la restricción FOREIGN KEY.|  
|PK_NAME|**sysname**|Identificador de la clave principal. Es NULL si no es aplicable al origen de datos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve el nombre de la restricción PRIMARY KEY.|  
  
 Los resultados devueltos se ordenan por FKTABLE_QUALIFIER, FKTABLE_OWNER, FKTABLE_NAME y KEY_SEQ.  
  
## <a name="remarks"></a>Comentarios  
 La codificación de aplicaciones que incluye tablas con claves externas deshabilitadas se puede implementar si:  
  
-   Se deshabilita temporalmente la comprobación de restricciones (ALTER TABLE NOCHECK o CREATE TABLE NOT FOR REPLICATION) mientras se trabaja con las tablas y, después, se vuelve a habilitar.  
  
-   Se utilizan desencadenadores o código de aplicación para exigir relaciones.  
  
Si se proporciona el nombre de tabla de la clave principal y el nombre de tabla de la clave externa es NULL, sp_fkeys devuelve todas las tablas que contengan una clave externa para la tabla dada. Si se proporciona el nombre de tabla de la clave externa y el nombre de tabla de la clave principal es NULL, sp_fkeys devuelve todas las tablas relacionadas mediante una relación de clave principal y clave externa con las claves externas de la tabla de claves externas.  
  
El procedimiento almacenado sp_fkeys es equivalente a SQLForeignKeys en ODBC.  
  
## <a name="permissions"></a>Permisos  
 Requiere `SELECT` permiso en el esquema.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se recupera una lista de claves externas de la tabla `HumanResources.Department` en la base de datos `AdventureWorks2012`.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_fkeys @pktable_name = N'Department'  
    ,@pktable_owner = N'HumanResources';  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo se recupera una lista de claves externas de la tabla `DimDate` en la base de datos `AdventureWorksPDW2012`. No se devuelven filas porque [!INCLUDE[ssDW](../../includes/ssdw-md.md)] no es compatible con las claves externas.  
  
```sql  
EXEC sp_fkeys @pktable_name = N'DimDate;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_pkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-pkeys-transact-sql.md)  
  
  

