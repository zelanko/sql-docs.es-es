---
title: Conjunto de filas DBSCHEMA_CATALOGS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DBSCHEMA_CATALOGS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_CATALOGS rowset
ms.assetid: f02dc75d-5442-4eea-b33a-567dc816be7a
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: fe0b9bd6fa59114d95720b4c0b5b631ea88c2748
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="dbschemacatalogs-rowset"></a>Conjunto de filas DBSCHEMA_CATALOGS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
