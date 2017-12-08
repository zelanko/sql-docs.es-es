---
title: Conjunto de filas DBSCHEMA_CATALOGS | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DBSCHEMA_CATALOGS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6e001700aab7f231e186576226ae97468572698d
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbschemacatalogs-rowset"></a>Conjunto de filas DBSCHEMA_CATALOGS
  Identifica los atributos físicos asociados a los catálogos que son accesibles desde el sistema de administración de bases de datos (DBMS).  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DBSCHEMA_CATALOGS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|255|Nombre del catálogo. No puede ser null.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción legible de la tabla.|  
|**ROLES**|**DBTYPE_WSTR**||Una lista delimitada por comas de roles a los que pertenece el usuario actual.<br /><br /> Un asterisco (\*) se incluye como una función de si el usuario actual es un servidor o un administrador de base de datos.<br /><br /> **Username** se anexa a **ROLES** si uno de los roles utiliza la seguridad dinámica.|  
|**DATE_MODIFIED**|**DBTYPE_DBTIMESTAMP**||Fecha de la última modificación del catálogo.|  
  
 El conjunto de filas se ordena en **CATALOG_NAME**.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DBSCHEMA_CATALOGS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema OLE DB](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  
