---
title: sp_indexoption (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9a7b0b048fa2c2e0e9087463e89d4a4264de20b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spindexoption-transact-sql"></a>sp_indexoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define los valores de la opción de bloqueo para índices clúster y no clúster definidos por el usuario o tablas sin ningún índice clúster.  
  
 El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] selecciona automáticamente el bloqueo de nivel de página, fila o tabla. No es necesario establecer estas opciones manualmente. **sp_indexoption** se proporciona para los usuarios expertos que saben con certeza que un tipo de bloqueo determinado siempre es apropiado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]En su lugar, use [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@IndexNamePattern=**] **'***table_or_index_name***'**  
 Es el nombre calificado o no calificado de una tabla o índice definidos por un usuario. *table_or_index_name* es **nvarchar(1035)**, no tiene ningún valor predeterminado. Las comillas solo son necesarias si se especifica un índice o nombre de tabla completo. Si se proporciona un nombre de tabla completo, incluido el nombre de la base de datos, el nombre de la base de datos debe ser el nombre de la base de datos actual. Si se especifica un nombre de tabla sin ningún índice, el valor de la opción especificada se define para todos los índices de dicha tabla y para la tabla misma si no existe ningún índice clúster.  
  
 [  **@OptionName =**] **'***option_name***'**  
 Es un nombre de opción de índice. *option_name* es **varchar (35)**, no tiene ningún valor predeterminado. *option_name* puede tener uno de los siguientes valores.  
  
|Valor|Description|  
|-----------|-----------------|  
|**AllowRowLocks**|Cuando el valor es TRUE, se permiten bloqueos de fila al obtener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila. Cuando es FALSE, no se utilizan bloqueos de fila. El valor predeterminado es TRUE.|  
|**AllowPageLocks**|Cuando el valor es TRUE, se permiten bloqueos de página al obtener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página. Cuando es FALSE, no se utilizan bloqueos de página. El valor predeterminado es TRUE.|  
|**DisAllowRowLocks**|Cuando es TRUE no se utilizan bloqueos de fila. Cuando el valor es FALSE, se permiten bloqueos de fila al obtener acceso al índice. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina cuándo se usan los bloqueos de fila.|  
|**DisAllowPageLocks**|Cuando es TRUE, no se utilizan bloqueos de página. Cuando el valor es FALSE, se permiten bloqueos de página al obtener acceso al índice. [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina el momento en que se usan los bloqueos de página.|  
  
 [  **@OptionValue =**] **'***valor***'**  
 Especifica si el *option_name* configuración está habilitado (TRUE, ON, yes o 1) o deshabilitado (FALSE, OFF, no o 0). *valor* es **varchar (12)**, no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o mayor que 0 (error)  
  
## <a name="remarks"></a>Comentarios  
 Los índices XML no se admiten. Si se especifica un índice XML o un nombre de tabla sin ningún nombre de índice y la tabla contiene un índice XML, la instrucción produce un error. Para establecer estas opciones, utilice [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) en su lugar.  
  
 Para mostrar la fila actual y la página de propiedades de bloqueo, utilice [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) o [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo.  
  
-   Fila, página y bloqueos de nivel de tabla se permiten al tener acceso al índice cuando **AllowRowLocks** = TRUE o **DisAllowRowLocks** = FALSE, y **AllowPageLocks** = TRUE o  **DisAllowPageLocks** = FALSE. [!INCLUDE[ssDE](../../includes/ssde-md.md)] elige el bloqueo apropiado y puede cambiar de escala el bloqueo: de un bloqueo de fila o página a un bloqueo de tabla.  
  
 Se permite únicamente un bloqueo de nivel de tabla al obtener acceso al índice cuando **AllowRowLocks** = FALSE o **DisAllowRowLocks** = TRUE y **AllowPageLocks** = FALSE o  **DisAllowPageLocks** = TRUE.  
  
 Si se especifica un nombre de tabla sin ningún índice, la configuración se aplica a todos los índices de esa tabla. Si la tabla subyacente no tiene ningún índice clúster (es decir, es un montón), la configuración se aplica de la siguiente manera:  
  
-   Cuando **AllowRowLocks** o **DisAllowRowLocks** está establecida en TRUE o FALSE, la configuración se aplica al montón y cualquier índice no clúster asociado.  
  
-   Cuando **AllowPageLocks** opción está establecida en TRUE o **DisAllowPageLocks** se establece en FALSE, la configuración se aplica al montón y cualquier índice no clúster asociado.  
  
-   Cuando **AllowPageLocks** opción está establecida en FALSE o **DisAllowPageLocks** está establecida en TRUE, la configuración se aplica por completo a los índices no clúster. Es decir, no se permite ningún bloqueo de página en los índices no clúster. En el montón, no se permiten únicamente los bloqueos compartidos (S), de actualización (U) y exclusivos (X) de la página. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] aún puede adquirir un bloqueo de página de intención (IS, IU o IX) por motivos internos.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER en la tabla.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. Definir una opción en un índice específico  
 El siguiente ejemplo deshabilita los bloqueos de página en el `IX_Customer_TerritoryID` de índice en el `Customer` tabla.  
  
```tsql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. Definir una opción en todos los índices de una tabla  
 El siguiente ejemplo no permite bloqueos de fila en los índices asociados con la tabla `Product`. La vista de catálogo `sys.indexes` se consulta antes y después de ejecutar el procedimiento `sp_indexoption` para mostrar los resultados de la instrucción.  
  
```tsql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. Definir una opción en una tabla sin clúster  
 El siguiente ejemplo no permite bloqueos de página en una tabla sin clúster (un montón). El `sys.indexes` se consulta la vista de catálogo antes y después de la `sp_indexoption` procedimiento se ejecuta para mostrar los resultados de la instrucción.  
  
```tsql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
