---
title: Conjunto de filas MDSCHEMA_INPUT_DATASOURCES | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_INPUT_DATASOURCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e105cc8151640f5d5d74d6c7c76cc52edc16a242
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemainputdatasources-rowset"></a>Conjunto de filas MDSCHEMA_INPUT_DATASOURCES
  Describe los orígenes de datos definidos dentro de la base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **MDSCHEMA_INPUT_DATASOURCES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||El nombre del catálogo al que pertenece este origen de datos.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||No compatible.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**||El nombre del objeto de origen de datos.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**||Tipo del origen de datos. Los valores válidos incluyen:<br /><br /> **Relacional**<br /><br /> **OLAP**|  
|**CREATED_ON**|**DBTYPE_DBTIMESTAMP**||Fecha de creación del origen de datos.|  
|**LAST_SCHEMA_UPDATE**|**DBTYPE_DBTIMESTAMP**||Fecha y hora de la última modificación del origen de datos.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Descripción fácil de comprender de la acción.|  
|**TIEMPO DE ESPERA**|**DBTYPE_UI4**||Tiempo de espera del origen de datos.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **MDSCHEMA_INPUT_DATASOURCES** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DATASOURCE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DATASOURCE_TYPE**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

