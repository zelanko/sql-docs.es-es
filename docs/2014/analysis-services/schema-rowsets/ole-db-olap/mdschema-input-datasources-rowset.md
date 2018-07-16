---
title: Conjunto de filas MDSCHEMA_INPUT_DATASOURCES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_INPUT_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_INPUT_DATASOURCES rowset
ms.assetid: 12482fd5-16e3-4171-9cb0-76d0d4f5308e
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aedd2980b6c51872a9d78d6d1c2cbbecc84d7ec4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249115"
---
# <a name="mdschemainputdatasources-rowset"></a>Conjunto de filas MDSCHEMA_INPUT_DATASOURCES
  Describe los orígenes de datos definidos dentro de la base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `MDSCHEMA_INPUT_DATASOURCES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre del catálogo al que pertenece este origen de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`||El nombre del objeto de origen de datos.|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`||Tipo del origen de datos. Los valores válidos incluyen:<br /><br /> -   `Relational`<br />-   `Olap`|  
|`CREATED_ON`|`DBTYPE_DBTIMESTAMP`||Fecha de creación del origen de datos.|  
|`LAST_SCHEMA_UPDATE`|`DBTYPE_DBTIMESTAMP`||Fecha y hora de la última modificación del origen de datos.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción fácil de comprender de la acción.|  
|`TIMEOUT`|`DBTYPE_UI4`||Tiempo de espera del origen de datos.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_INPUT_DATASOURCES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DATASOURCE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DATASOURCE_TYPE`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
