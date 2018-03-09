---
title: sp_help_spatial_geometry_histogram (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_histogram
- sp_help_spatial_geometry_histogram_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_histogram
ms.assetid: 036aaf61-df3e-40f7-aa4e-62983c5a37bd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5acd841815df5329fe79624174c00e2694e65781
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpspatialgeometryhistogram-transact-sql"></a>sp_help_spatial_geometry_histogram (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Facilita la introducción de los parámetros del cuadro de límite y de la cuadrícula para un índice espacial.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_spatial_geometry_histogram [ @tabname =] 'tabname'   
     [ , [ @colname = ] 'columnname' ]   
     [ , [ @resolution = ] 'resolution' ]  
     [ , [ @xmin = ] 'minx' ]   
     [ , [ @ymin = ] 'miny' ]   
     [ ,.[ @xmax = ] 'maxx' ]  
     [ , [ @ymax = ] 'maxy' ]  
     [ , [ @sample = ] 'sample' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@tabname =**] **'***tabname***'**  
 Es el nombre completo o incompleto de la tabla para la que se ha especificado el índice espacial.  
  
 Se requieren comillas únicamente si se especifica una tabla certificada. Si se proporciona un nombre completo, incluido el nombre de la base de datos, el nombre de la base de datos debe ser el de la base de datos actual. *TabName* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@colname =** ] **'***colname***'**  
 Es el nombre de la columna espacial especificada. *colname* es un **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@resolution =** ] **'***resolución***'**  
 Es la resolución del cuadro de límite. Los valores válidos van del 10 al 5000. *resolución* es un **tinyint**, no tiene ningún valor predeterminado.  
  
 [  **@xmin =** ] **'***xmin***'**  
 Es la propiedad del cuadro de límite X mínimo. *XMIN* es un **float**, no tiene ningún valor predeterminado.  
  
 [  **@ymin =** ] **'***ymin***'**  
 Es la propiedad del cuadro de límite Y mínimo. *YMIN* es un **float**, no tiene ningún valor predeterminado.  
  
 [  **@xmax =** ] **'***xmax***'**  
 Es la propiedad del cuadro de límite X máximo. *XMAX* es un **float**, no tiene ningún valor predeterminado.  
  
 [  **@ymax =** ] **'***ymax***'**  
 Es la propiedad del cuadro de límite Y máximo. *YMAX* es un **float**, no tiene ningún valor predeterminado.  
  
 [  **@sample =** ] **'***ejemplo***'**  
 Es el porcentaje de la tabla que se usa. Los valores válidos son de 0 a 100. *ejemplo* es un **float**. Valor predeterminado es 100.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad/Valor devuelto  
 Se devuelve un valor de tabla. En la siguiente cuadrícula se describe el contenido de la columna de la tabla.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**cellid**|**int**|Representa el identificador único de cada celda, el recuento empieza por 1.|  
|**celda**|**geometry**|Es un polígono rectangular que representa cada celda. La forma de la celda es idéntica a la de la celda usada para los índices espaciales.|  
|**row_count**|**bigint**|Indica el número de objetos espaciales que tocan la celda o que están contenidos en ella.|  
  
## <a name="permissions"></a>Permissions  
 Usuario debe ser un miembro de la **público** rol. Requiere el permiso READ ACCESS en el servidor y el objeto.  
  
## <a name="remarks"></a>Comentarios  
 La pestaña Resultados espaciales de SSMS muestra una representación gráfica de los resultados. Puede consultar los resultados en la ventana espacial para obtener un número aproximado de elementos de resultados. Los objetos de la tabla pueden ocupar más de una celda. Por tanto, la suma de las celdas puede ser mayor que el número de objetos reales.  
  
 Puede que se agregue una fila adicional al conjunto de resultados que contiene el número de objetos situados fuera del cuadro de límite o que están en contacto con el borde de dicho cuadro. El **cellid** de esta fila es 0 y el **celda** de esta fila contiene un **LineString** que representa el cuadro de límite. Esta fila representa todo el espacio fuera del cuadro de límite.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se crea una tabla de ejemplo y, a continuación, llama **sp_help_spatial_geometry_histogram** en la tabla.  
  
 `USE AdventureWorksDW2012`  
  
 `GO`  
  
 `-- Set database compatibility for circular arc segments`  
  
 `ALTER DATABASE AdventureWorksDW2012`  
  
 `SET COMPATIBILITY_LEVEL = 110;`  
  
 `GO`  
  
 `-- Create table to execute sp_help_spatial_geometry_histogram on`  
  
 `CREATE TABLE TownSites`  
  
 `(`  
  
 `Location geometry NULL,`  
  
 `SiteName nvarchar(50) NULL`  
  
 `)`  
  
 `GO`  
  
 `-- Insert site data into table`  
  
 `DECLARE @g geometry;`  
  
 `SET @g = geometry::Parse('POINT(0 0)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Booth Map';`  
  
 `SET @g = geometry::Parse('POLYGON((1 1, 1 2, 2 2, 2 1, 1 1))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Town Hall';`  
  
 `SET @g = geometry::Parse('CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(-1 0, 0 -1, 1 0),(1 0, 1 2, -1 0)))');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Park';`  
  
 `SET @g = geometry::Parse('CIRCULARSTRING(1 5, 2 2, 5 1)');`  
  
 `INSERT INTO TownSites(Location, SiteName)`  
  
 `SELECT @g, N'Main Road';`  
  
 `-- Call proc to see data within bounding box`  
  
 `EXEC sp_help_spatial_geometry_histogram @tabname = TownSites, @colname = Location, @resolution = 64, @xmin = -2, @ymin = -2, @xmax = 3, @ymax = 3, @sample = 100;`  
  
 `GO`  
  
 `DROP TABLE TownSites;`  
  
 `GO`  
  
## <a name="see-also"></a>Vea también  
 [Índice espacial almacenados procedimientos &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)  
  
  
