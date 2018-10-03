---
title: Conjunto de filas DISCOVER_INSTANCES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_INSTANCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8a0f716f32898668e019db15aef62e140e9c0d09
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48198599"
---
# <a name="discoverinstances-rowset"></a>Conjunto de filas DISCOVER_INSTANCES
  Describe las instancias en el servidor.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_INSTANCES` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`INSTANCE_NAME`|`DBTYPE_WSTR`||Nombre de la instancia.|  
|`INSTANCE_PORT_NUMBER`|`DBTYPE_I4`||El número de puerto en que escucha la instancia.|  
|`INSTANCE_STATE`|`DBTYPE_I4`||Estado de instancia del servidor:<br /><br /> -   `Started`<br />-   `Stopped`<br />-   `Starting`<br />-   `Stopping`<br />-   `Paused`|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_INSTANCES` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`INSTANCE_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Vea también  
 [OLE DB para los conjuntos de filas de esquema OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
