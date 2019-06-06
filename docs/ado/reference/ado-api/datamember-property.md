---
title: Propiedad DataMember | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9de69478469a6bd177d12beab96e199b4720f3f5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695487"
---
# <a name="datamember-property"></a>Propiedad DataMember
Indica el nombre del miembro de datos que se recuperan desde el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) hace referencia a él la [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) propiedad.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **cadena** valor. El nombre no distingue mayúsculas de minúsculas.  
  
## <a name="remarks"></a>Comentarios  
 Esta propiedad se utiliza para crear controles enlazados a datos con el entorno de datos. El entorno de datos mantiene las colecciones de datos (orígenes de datos) que contiene objetos con nombre (miembros de datos) que se representará como un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto.  
  
 El **DataMember** y **DataSource** propiedades deben usarse juntas.  
  
 El **DataMember** propiedad determina qué objeto especificado por el **DataSource** propiedad se representará como un **Recordset** objeto. El **Recordset** objeto debe estar cerrado antes de establecer esta propiedad. Se genera un error si el **DataMember** no se establece la propiedad antes de la **DataSource** propiedad, o si el **DataMember** no se reconoce el nombre por el objeto especificado en el **DataSource** propiedad.  
  
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
