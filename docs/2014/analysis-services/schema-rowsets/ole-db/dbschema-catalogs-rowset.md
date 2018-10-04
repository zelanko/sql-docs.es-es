---
title: Conjunto de filas DBSCHEMA_CATALOGS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DBSCHEMA_CATALOGS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f9c503d60de405836d90938caa6bff10f96378a1
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163235"
---
# <a name="dbschemacatalogs-rowset"></a>Conjunto de filas DBSCHEMA_CATALOGS
  Identifica los atributos físicos asociados a los catálogos que son accesibles desde el sistema de administración de bases de datos (DBMS).  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DBSCHEMA_CATALOGS` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|255|Nombre del catálogo. No puede ser null.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción legible de la tabla.|  
|`ROLES`|`DBTYPE_WSTR`||Una lista delimitada por comas de roles a los que pertenece el usuario actual.<br /><br /> Un asterisco (\*) se incluye como una función de si el usuario actual es un servidor o un administrador de base de datos.<br /><br /> `Username` se anexa a `ROLES` si uno de los roles utiliza la seguridad dinámica.|  
|`DATE_MODIFIED`|`DBTYPE_DBTIMESTAMP`||Fecha de la última modificación del catálogo.|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DBSCHEMA_CATALOGS` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema OLE DB](ole-db-schema-rowsets.md)  
  
  
