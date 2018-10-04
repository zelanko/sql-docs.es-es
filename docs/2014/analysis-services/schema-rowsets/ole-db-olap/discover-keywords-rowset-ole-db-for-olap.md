---
title: Conjunto de filas DISCOVER_KEYWORDS (OLE DB para OLAP) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_KEYWORDS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_KEYWORDS rowset
ms.assetid: 70cc680d-9530-469b-8a61-4e6779aec17a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8fb1249cb328aac0e24d74b1ab53a4def09c4646
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130979"
---
# <a name="discoverkeywords-rowset-ole-db-for-olap"></a>Conjunto de filas DISCOVER_KEYWORDS (OLE DB para OLAP)
  Enumera una lista de palabras reservada por el proveedor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas DISCOVER_KEYWORDS contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`Keyword`|`DBTYPE_WSTR`||Una palabra clave reservada.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas DISCOVER_KEYWORDS puede estar restringido en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`Keyword`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
