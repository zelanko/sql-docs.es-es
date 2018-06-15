---
title: Propiedad DataMember | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d194cea2dd1a7bbabf8acd2e9d89945772eddd31
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35277414"
---
# <a name="datamember-property"></a>Propiedad DataMember
Indica el nombre del miembro de datos que se recuperará de la [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) referenciado por la [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) propiedad.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor. El nombre no distingue mayúsculas de minúsculas.  
  
## <a name="remarks"></a>Notas  
 Esta propiedad se utiliza para crear controles enlazados a datos con el entorno de datos. El entorno de datos mantiene colecciones de datos (orígenes de datos) que contiene objetos con nombre (miembros de datos) que se representarán como un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
 El **DataMember** y **DataSource** propiedades se deben usar conjuntamente.  
  
 El **DataMember** propiedad determina qué objeto especificado por el **DataSource** propiedad se representará como una **Recordset** objeto. El **Recordset** objeto debe estar cerrado antes de establece esta propiedad. Se genera un error si la **DataMember** propiedad no se establece antes de la **DataSource** propiedad, o si la **DataMember** no se reconoce el nombre por el objeto especificado en el **DataSource** propiedad.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad de origen de datos (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
