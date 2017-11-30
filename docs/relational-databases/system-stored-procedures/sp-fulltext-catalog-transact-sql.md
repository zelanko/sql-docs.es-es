---
title: sp_fulltext_catalog (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs: TSQL
helpviewer_keywords: sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
caps.latest.revision: "37"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7fe79eb04fba828a21d32328cd32fc5db7645202
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="spfulltextcatalog-transact-sql"></a>sp_fulltext_catalog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea y quita un catálogo de texto completo, e inicia y detiene la acción de indización de un catálogo. Se pueden crear varios catálogos de texto completo en cada base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md), [ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md), y [DROP FULLTEXT CATALOG](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) en su lugar.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@ftcat=**] **'***fulltext_catalog_name***'**  
 Es el nombre del catálogo de texto completo. Los nombres de catálogo deben ser únicos en cada base de datos. *fulltext_catalog_name* es **sysname**.  
  
 [  **@action=**] **'***acción***'**  
 Se trata de la acción que se va a realizar. *acción* es **varchar (20)**, y puede tener uno de estos valores.  
  
> [!NOTE]  
>  Los catálogos de texto completo se pueden crear, quitar o modificar como precise. No obstante, evite realizar cambios de esquema en varios catálogos al mismo tiempo. Estas acciones pueden realizarse usando el **sp_fulltext_table** procedimiento almacenado, que es el método recomendado.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Crear**|Crea un catálogo de texto completo vacío, nueva en el sistema de archivos y agrega una fila asociada en **sysfulltextcatalogs** con el *fulltext_catalog_name* y *root_directory*, Si está presente, los valores. *fulltext_catalog_name* debe ser único dentro de la base de datos.|  
|**Drop**|Quita *fulltext_catalog_name* quitando del sistema de archivos y eliminar la fila asociada en **sysfulltextcatalogs**. Esta acción genera un error si el catálogo contiene índices de una o más tablas. **sp_fulltext_table** '*table_name*', 'drop' debe ejecutarse para quitar las tablas del catálogo.<br /><br /> Se muestra un error si el catálogo no existe.|  
|**start_incremental**|Inicia un llenado incremental de *fulltext_catalog_name*. Se muestra un error si el catálogo no existe. Si ya hay un rellenado de índices de texto completo activo, se muestra una advertencia y no se produce el rellenado. Rellenado incremental sólo las filas modificadas se recuperan para la indización de texto completo, suponiendo que haya una **marca de tiempo** las columnas presentes en la tabla de texto completo indizadas.|  
|**start_full**|Inicia un rellenado completo para *fulltext_catalog_name*. Se recupera cada una de las filas de todas las tablas asociadas con este catálogo de texto para realizar la indización de texto, aunque ya se hayan indizado.|  
|**Detener**|Detiene un llenado de índice de *fulltext_catalog_name*. Se muestra un error si el catálogo no existe. No se muestra ninguna advertencia si el rellenado ya se ha detenido.|  
|**Volver a generar**|Vuelve a generar *fulltext_catalog_name*. Cuando vuelve a generarse un catálogo, el catálogo existente se elimina y se crea uno nuevo en su lugar. Todas las tablas que tienen referencias de índices de texto completo se asocian al catálogo nuevo. La regeneración restablece los metadatos de texto completo de las tablas del sistema de la base de datos.<br /><br /> Si el seguimiento de cambios está establecido en OFF, la regeneración no hace que se vuelva a rellenar el catálogo de texto completo recién creado. En este caso, para volver a llenar, ejecute **sp_fulltext_catalog** con el **start_full** o **start_incremental** acción.|  
  
 [  **@path=**] **'***root_directory***'**  
 Es el directorio raíz (no la ruta física completa) de un **crear** acción. *root_directory* es **nvarchar (100)** y tiene un valor predeterminado es null, lo que indica el uso de la ubicación predeterminada especificada al realizar la instalación. Esto es el subdirectorio Ftdata del directorio Mssql; Por ejemplo, C:\Program Files\Microsoft SQL Server\MSSQL13. MSSQLSERVER\MSSQL\FTData. El directorio raíz especificado debe existir, residir en una unidad en el mismo equipo y constar de más datos que solo la letra de unidad, y no puede ser una ruta de acceso relativa. No se admiten las unidades de red, discos extraíbles, disquetes y rutas de acceso UNC. Los catálogos de texto completo deben crearse en una unidad de disco duro local asociada con una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **@path**solo es válido cuando *acción* es **crear**. Para acciones distintas a **crear** (**detener**, **volver a generar**, etc.),  **@path**  debe ser NULL o se omite.  
  
 Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un servidor virtual en un clúster, el directorio del catálogo especificado debe estar en una unidad de disco compartida de la que depende el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si @path no se especifica, la ubicación del directorio del catálogo de forma predeterminada está en la unidad de disco compartida, en el directorio que se especificó cuando se instaló el servidor virtual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 El **start_full** acción se usa para crear una instantánea completa de los datos de texto completo en *fulltext_catalog_name*. El **start_incremental** acción se usa para volver a indizar sólo las filas modificadas en la base de datos. Rellenado incremental se puede aplicar sólo si la tabla tiene una columna de tipo **marca de tiempo**. Si una tabla en el catálogo de texto completo no contiene una columna de tipo **marca de tiempo**, la tabla se somete a un llenado completo.  
  
 Los datos del catálogo de texto completo y del índice se almacenan en archivos creados en un directorio de catálogos de texto completo. El directorio del catálogo de texto completo se crea como un subdirectorio del directorio especificado en  **@path**  o en el directorio de catálogo de texto completo predeterminado de servidor si  **@path**  no es especificado. El nombre del directorio de catálogos de texto completo se genera de forma que se garantiza que será exclusivo en el servidor. Por lo tanto, todos los directorios de catálogos de texto completo de un servidor pueden compartir la misma ruta de acceso.  
  
## <a name="permissions"></a>Permissions  
 El llamador debe ser miembro de la **db_owner** rol. Según la acción solicitada, el autor de llamada no se debe denegar los permisos ALTER o CONTROL (que **db_owner** tiene) en el catálogo de texto completo de destino.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-create-a-full-text-catalog"></a>A. Crear un catálogo de texto completo  
 Este ejemplo crea un catálogo de texto completo vacío, **Cat_Desc**, en la **AdventureWorks2012** base de datos.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. Para regenerar un catálogo de texto completo  
 En este ejemplo se vuelve a generar un catálogo de texto completo existente, **Cat_Desc**, en la **AdventureWorks2012** base de datos.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. Iniciar el rellenado de un catálogo de texto completo  
 Este ejemplo inicia un rellenado completo de la **Cat_Desc** catálogo.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. Detener el rellenado de un catálogo de texto completo  
 En este ejemplo se detiene el rellenado de la **Cat_Desc** catálogo.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. Quitar un catálogo de texto completo  
 Este ejemplo quita la **Cat_Desc** catálogo.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [FULLTEXTCATALOGPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
