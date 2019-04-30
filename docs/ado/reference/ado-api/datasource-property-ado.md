---
title: Propiedad de origen de datos (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad42ea14e58e28bf5eee0e5aac66c5a8fc309f2f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63140126"
---
# <a name="datasource-property-ado"></a>Propiedad de origen de datos (ADO)
Indica un objeto que contiene los datos que se puede representar como un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad se utiliza para crear controles enlazados a datos con el entorno de datos. El entorno de datos mantiene las colecciones de datos (orígenes de datos) que contiene objetos con nombre (miembros de datos) que se representará como un **Recordset** objeto *.*  
  
 El [DataMember](../../../ado/reference/ado-api/datamember-property.md) y **DataSource** propiedades deben utilizarse conjuntamente.  
  
 El objeto al que hace referencia debe implementar la **IDataSource** interfaz y debe contener un **IRowset** interfaz.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad DataMember](../../../ado/reference/ado-api/datamember-property.md)
