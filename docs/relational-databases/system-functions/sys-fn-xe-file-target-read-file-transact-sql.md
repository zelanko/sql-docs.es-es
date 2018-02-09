---
title: sys.fn_xe_file_target_read_file (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/22/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_xe_file_target_read_file_TSQL
- fn_xe_file_target_read_file
- sys.fn_xe_file_target_read_file_TSQL
- sys.fn_xe_file_target_read_file
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], functions
- fn_xe_file_target_read_file function
- sys.fn_xe_file_target_read_file function
ms.assetid: cc0351ae-4882-4b67-b0d8-bd235d20c901
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 6284bd7690c715ed47177b42a5a1f5beb4b4b6a3
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sysfnxefiletargetreadfile-transact-sql"></a>sys.fn_xe_file_target_read_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Lee los archivos creados en el destino de archivo asincrónico de Eventos extendidos. Se devuelve un evento, en formato XML, por cada fila.  
  
> [!WARNING]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] aceptan resultados de seguimiento generados en formato XEL y XEM. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]Extendidos solo son compatibles con los eventos en los resultados de seguimiento en formato XEL. Es recomendable que use SQL Server Management Studio para leer los resultados de seguimiento en formato XEL.    
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_xe_file_target_read_file ( path, mdpath, initial_file_name, initial_offset )  
```  
  
## <a name="arguments"></a>Argumentos  
 *path*  
 Ruta de acceso a los archivos que se van a leer. *ruta de acceso* puede contener caracteres comodín e incluir el nombre de un archivo. *ruta de acceso* es **nvarchar (260)**. No tiene ningún valor predeterminado. En el contexto de base de datos de SQL Azure, este valor es una dirección URL HTTP en un archivo en el almacenamiento de Azure.
  
 *mdpath*  
 La ruta de acceso al archivo de metadatos que corresponde al archivo o archivos especificados por el *ruta de acceso* argumento. *mdpath* es **nvarchar (260)**. No tiene ningún valor predeterminado. A partir de SQL Server 2016, este parámetro puede indicarse como null.
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] no requiere la *mdpath* parámetro. Sin embargo, se mantiene para la compatibilidad con versiones anteriores para los archivos de registro generados en versiones anteriores de SQL Server.  
  
 *initial_file_name*  
 El primer archivo para leer de *ruta de acceso*. *initial_file_name* is **nvarchar(260)**. No tiene ningún valor predeterminado. Si **null** se especifica como el argumento de todos los archivos que se encuentran en *ruta de acceso* se leen.  
  
> [!NOTE]  
>  *initial_file_name* y *initial_offset* son argumentos emparejados. Si especifica un valor para cualquiera de ellos, debe especificar un valor para el otro.  
  
 *initial_offset*  
 Se usa para especificar el último desplazamiento leído previamente y omite todos los eventos hasta el desplazamiento (incluido). La enumeración de eventos comienza después del desplazamiento especificado. *initial_offset* es **bigint**. Si **null** no se especifica como el argumento de todo el archivo se leerán.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|module_guid|**uniqueidentifier**|GUID del módulo de eventos. No admite valores NULL.|  
|package_guid|**uniqueidentifier**|GUID del paquete de eventos. No admite valores NULL.|  
|object_name|**nvarchar(256)**|Nombre del evento. No admite valores NULL.|  
|event_data|**nvarchar(max)**|Contenido del evento, en formato XML. No admite valores NULL.|  
|file_name|**nvarchar(260)**|Nombre del archivo que contiene el evento. No admite valores NULL.|  
|file_offset|**bigint**|Desplazamiento del bloque en el archivo que contiene el evento. No admite valores NULL.|  
|timestamp_utc|**datetime2**|**Se aplica a**: [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].<br /><br />La fecha y hora (zona horaria UTC) del evento. No admite valores NULL.|  

  
## <a name="remarks"></a>Comentarios  
 Leer resultados grandes establece ejecutando **sys.fn_xe_file_target_read_file** en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] puede producir un error. Use la **resultados a archivo** modo (**Ctrl + Mayús + F**) para exportar grandes conjuntos de resultados a un archivo y leer el archivo con otra herramienta en su lugar.  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-retrieving-data-from-file-targets"></a>A. Recuperar datos de los destinos de archivo  
 En el ejemplo siguiente se obtienen todas las filas de todos los archivos. En este ejemplo, los destinos de archivo y metarchivos se encuentran en la carpeta de seguimientos en la unidad C:\.  
  
```  
SELECT * FROM sys.fn_xe_file_target_read_file('C:\traces\*.xel', 'C:\traces\metafile.xem', null, null);  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas de administración dinámica de eventos extendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Vistas de catálogo de eventos extendidos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
  
