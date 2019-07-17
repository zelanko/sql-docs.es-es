---
title: Sys.dm_clr_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7d7f5959eaacc9e25f7a80d338bcdac0bed59cff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138403"
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Devuelve una fila para cada propiedad relacionada con la integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Common Language Runtime (CLR), incluidos la versión y el estado del entorno CLR hospedado. El entorno CLR hospedado se inicializa mediante la ejecución de la [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md), o [DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md) instrucciones, o ejecutando cualquier rutina, tipo o desencadenador CLR. El **sys.dm_clr_properties** vista no especifica si se ha habilitado la ejecución de código CLR de usuario en el servidor. La ejecución de código CLR de usuario se habilita mediante el uso de la [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) procedimiento almacenado con el [clr habilitado](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) opción establecido en 1.  
  
 El **sys.dm_clr_properties** vista contiene la **nombre** y **valor** columnas. Cada una de las filas de esta vista proporciona información detallada acerca de una propiedad del entorno CLR hospedado. Utilice esta vista para recopilar información acerca del entorno CLR hospedado, como el directorio de instalación de CLR, la versión de CLR y el estado actual del entorno CLR hospedado. Esta vista puede ayudarle a determinar si el código de integración CLR no funciona debido a problemas con la instalación de CLR en el equipo servidor.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|El nombre de la propiedad.|  
|**value**|**nvarchar(128)**|Valor de la propiedad.|  
  
## <a name="properties"></a>Propiedades  
 El **directory** propiedad indica el directorio que se instaló .NET Framework en el servidor. Podría haber varias instalaciones de .NET Framework en el equipo servidor y el valor de esta propiedad identificaría la instalación que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estaría utilizando.  
  
 El **versión** propiedad indica la versión de .NET Framework y entorno CLR hospedado en el servidor.  
  
 El **sys.dm_clr_properties** vista de administración dinámica puede devolver seis valores distintos para el **estado** propiedad, que refleja el estado de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entorno CLR hospedado. Estas sobrecargas son:  
  
-   Mscoree is not loaded.  
  
-   Mscoree is loaded.  
  
-   Locked CLR version with mscoree.  
  
-   CLR is initialized.  
  
-   CLR initialization permanently failed.  
  
-   CLR is stopped.  
  
 El **Mscoree no está cargado** y **se carga Mscoree** Estados muestran la progresión de la inicialización del entorno CLR hospedada en el inicio del servidor y no es probables que se ha visto.  
  
 El **versión CLR bloqueado con mscoree** estado puede verse donde no se usa el entorno CLR hospedado y, por lo tanto, aún no ha se ha inicializado. El entorno CLR hospedado se inicializa por primera vez una instrucción DDL (como [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) o un objeto de base de datos administrado se ejecuta.  
  
 El **se inicializa CLR** estado indica que el entorno CLR hospedado se inicializó correctamente. Tenga en cuenta que esto no indica si se ha habilitado la ejecución de código CLR de usuario. Si la ejecución de código CLR de usuario es el primera habilitado y, a continuación, se deshabilita mediante la [!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) procedimiento almacenado, el valor de estado se seguirá **se inicializa CLR**.  
  
 El **permanentemente error de inicialización de CLR** estado indica que entorno CLR hospedado error de inicialización. Una causa probable es la presión de memoria, o también podría ser el resultado de un error del protocolo de enlace de hospedaje entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el entorno CLR. En este caso se producirá el mensaje de error 6512 o 6513.  
  
 El **CLR se detiene estado** solo se produce cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es está cerrando.  
  
## <a name="remarks"></a>Comentarios  
 Pueden cambiar las propiedades y valores de esta vista en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debido a las mejoras de la funcionalidad de integración de CLR.  
  
## <a name="permissions"></a>Permisos  
  
En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el permiso `VIEW DATABASE STATE` en la base de datos.   

## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se recupera información acerca del entorno CLR hospedado:  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con el Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
