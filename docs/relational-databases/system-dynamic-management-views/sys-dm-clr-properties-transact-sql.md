---
title: sys.dm_clr_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1f26f5870db7794bb52da665a17a3f70198fc341
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Devuelve una fila para cada propiedad relacionada con la integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Common Language Runtime (CLR), incluidos la versión y el estado del entorno CLR hospedado. El CLR hospedado se inicializa mediante la ejecución de la [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md), o [DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md) instrucciones, o ejecutando cualquier rutina CLR, el tipo o el desencadenador. El **sys.dm_clr_properties** vista no especifica si se ha habilitado la ejecución de código CLR de usuario en el servidor. Ejecución de código CLR de usuario se habilita utilizando la [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) procedimiento almacenado con el [clr habilitado](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) opción establecido en 1.  
  
 El **sys.dm_clr_properties** vista contiene la **nombre** y **valor** columnas. Cada una de las filas de esta vista proporciona información detallada acerca de una propiedad del entorno CLR hospedado. Utilice esta vista para recopilar información acerca del entorno CLR hospedado, como el directorio de instalación de CLR, la versión de CLR y el estado actual del entorno CLR hospedado. Esta vista puede ayudarle a determinar si el código de integración CLR no funciona debido a problemas con la instalación de CLR en el equipo servidor.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**nvarchar(128)**|El nombre de la propiedad.|  
|**value**|**nvarchar(128)**|Valor de la propiedad.|  
  
## <a name="properties"></a>Propiedades  
 El **directory** propiedad indica el directorio en el que se instaló .NET Framework en el servidor. Podría haber varias instalaciones de .NET Framework en el equipo servidor y el valor de esta propiedad identificaría la instalación que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estaría utilizando.  
  
 El **versión** propiedad indica la versión de .NET Framework y entorno CLR hospedado en el servidor.  
  
 El **sys.dm_clr_properties** vista de administración dinámica puede devolver seis valores distintos para la **estado** propiedad, que refleja el estado de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entorno CLR hospedado. Estas sobrecargas son:  
  
-   Mscoree is not loaded.  
  
-   Mscoree is loaded.  
  
-   Locked CLR version with mscoree.  
  
-   CLR is initialized.  
  
-   CLR initialization permanently failed.  
  
-   CLR is stopped.  
  
 El **Mscoree no está cargado** y **se carga Mscoree** Estados muestran la progresión de la inicialización del entorno CLR hospedada en el inicio del servidor y no es probable que se vean.  
  
 El **versión de CLR bloqueado con mscoree** estado puede aparecer en el entorno CLR hospedado no se utiliza y, por lo tanto, no se ha se ha inicializado. El CLR hospedado se inicializa la primera vez que una instrucción DDL (como [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) o se ejecuta un objeto de base de datos administrados.  
  
 El **se inicializa el CLR** estado indica que el entorno CLR hospedado se ha inicializado correctamente. Tenga en cuenta que esto no indica si se ha habilitado la ejecución de código CLR de usuario. Si la ejecución de código CLR de usuario es el primera habilitado y deshabilitado, a continuación, usar el [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) procedimiento almacenado, el valor de estado se seguirá **se inicializa el CLR**.  
  
 El **permanentemente error al inicializar el CLR** estado indica que hospeda CLR error de inicialización. Una causa probable es la presión de memoria, o también podría ser el resultado de un error del protocolo de enlace de hospedaje entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el entorno CLR. En este caso se producirá el mensaje de error 6512 o 6513.  
  
 El **CLR se detiene estado** solo se produce cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en el proceso que se va a cerrar.  
  
## <a name="remarks"></a>Comentarios  
 Pueden cambiar las propiedades y los valores de esta vista en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debido a las mejoras de la funcionalidad de integración de CLR.  
  
## <a name="permissions"></a>Permissions  
  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se recupera información acerca del entorno CLR hospedado:  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con el Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
