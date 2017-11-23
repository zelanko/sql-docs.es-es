---
title: sp_help_fulltext_catalogs_cursor (Transact-SQL) | Documentos de Microsoft
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
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1d6bafa75fc4962ee9b7c263f8fc08204da67fd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpfulltextcatalogscursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Utiliza un cursor para devolver el identificador, nombre, directorio raíz, estado y número de las tablas indizadas de texto completo para el catálogo de texto completo especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use la [sys.fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) vista de catálogo en su lugar.  
  
||  
|-|  
|**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@cursor_return=**]  *@cursor_variable*  **SALIDA**  
 Es la variable de salida de tipo **cursor**. El cursor es desplazable, dinámico y de solo lectura.  
  
 [  **@fulltext_catalog_name=**] **'***fulltext_catalog_name***'**  
 Es el nombre del catálogo de texto completo. *fulltext_catalog_name* es **sysname**. Si este parámetro se omite o tiene el valor NULL, se devuelve información acerca de todos los catálogos de texto completo asociados a la base de datos actual.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|Identificador del catálogo de texto completo.|  
|**NOMBRE**|**sysname**|Nombre del catálogo de texto completo.|  
|**RUTA DE ACCESO**|**nvarchar (260)**|A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], esta cláusula no tiene ningún efecto.|  
|**ESTADO**|**int**|Estado de rellenado del índice de texto completo del catálogo:<br /><br /> 0 = Inactivo<br /><br /> 1 = Rellenado completo en curso<br /><br /> 2 = En pausa<br /><br /> 3 = Acelerado<br /><br /> 4 = En recuperación<br /><br /> 5 = Apagado<br /><br /> 6 = Rellenado incremental en curso<br /><br /> 7 = Generación del índice<br /><br /> 8 = El disco está lleno. En pausa<br /><br /> 9 = Seguimiento de cambios|  
|**NUMBER_FULLTEXT_TABLES**|**int**|Número de tablas con índice de texto completo asociadas al catálogo.|  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, los permisos de ejecución corresponden al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se devuelve información acerca del catálogo de texto completo `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Vea también  
 [FULLTEXTCATALOGPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
