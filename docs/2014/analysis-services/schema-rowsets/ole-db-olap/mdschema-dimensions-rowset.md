---
title: Conjunto de filas MDSCHEMA_DIMENSIONS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDSCHEMA_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b00b617adf90e1dba8eac94a9872ce07c0773e7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105496"
---
# <a name="mdschemadimensions-rowset"></a>Conjunto de filas MDSCHEMA_DIMENSIONS
  Describe las dimensiones compartidas y privadas dentro de una base de datos.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas `MDSCHEMA_DIMENSIONS` contiene las siguientes columnas:  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||El nombre de la base de datos.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||No compatible.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Nombre del cubo.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||Nombre de la dimensión. Si una dimensión forma parte de más de un cubo o grupo de medidas, existe una fila para cada combinación única de dimensión, grupo de medidas y cubo.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||El nombre único de la dimensión.|  
|`DIMENSION_GUID`|`DBTYPE_GUID`||No compatible.|  
|`DIMENSION_CAPTION`|`DBTYPE_WSTR`||Título de la dimensión. Se debería utilizar al mostrar el nombre de la dimensión al usuario, como en la interfaz de usuario o en los informes.|  
|`DIMENSION_ORDINAL`|`DBTYPE_UI4`||Posición de la dimensión en el cubo.|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||El tipo de la dimensión. Los valores válidos incluyen:<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`DIMENSION_CARDINALITY`|`DBTYPE_UI4`||Número de miembros del atributo clave.|  
|`DEFAULT_HIERARCHY`|`DBTYPE_WSTR`||Una jerarquía de la dimensión. Se conserva para la compatibilidad con versiones anteriores.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Descripción fácil de comprender de la dimensión.|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||Siempre `FALSE`.|  
|`IS_READWRITE`|`DBTYPE_BOOL`||Un valor booleano que indica si la dimensión tiene permiso de escritura.<br /><br /> `TRUE` si la dimensión tiene permiso de escritura.|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||Un mapa de bits que especifica las columnas que contienen valores únicos, si la dimensión solo contiene miembros con nombres únicos. Las siguientes constantes de valor de bits se definen en Msmd.h para este mapa de bits:<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE`|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||Siempre `NULL`.|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||Siempre `TRUE`. **Nota:** una dimensión no está visible, a menos que una o más jerarquías en la dimensión están visibles.|  
  
 El conjunto de filas se ordena en `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_NAME`.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `MDSCHEMA_DIMENSIONS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -CUBO 1<br />-DIMENSIÓN DE 2<br /><br /> La restricción predeterminada es un valor de 1.|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|(Opcional) Mapa de bits con uno de los siguientes valores válidos:<br /><br /> -1 Visible<br />-2 no visible<br /><br /> La restricción predeterminada es un valor de 1.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  