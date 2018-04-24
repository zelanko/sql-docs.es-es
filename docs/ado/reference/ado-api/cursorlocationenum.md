---
title: CursorLocationEnum | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e5dc3fa4f78881502f846e828484ea03329d91e
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Especifica la ubicación del servicio de cursor.  
  
|Constante|Value|Description|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Utiliza cursores de cliente suministrados por una biblioteca de cursores locales. Servicios de cursores locales a menudo le permitirá muchas características que los cursores suministrados por controlador no podrán, por lo que esta configuración puede proporcionar una ventaja con respecto a las características que se habilitarán. Por compatibilidad con versiones anteriores, el sinónimo **adUseClientBatch** también se admite.|  
|**adUseNone**|1|No utiliza servicios de cursor. (Esta constante está obsoleta y aparece únicamente por motivos de compatibilidad con versiones anteriores).|  
|**adUseServer**|2|Predeterminado: Utiliza cursores suministrados por el proveedor de datos o el controlador. Estos cursores a veces son muy flexibles y permiten sensibilidad adicional a los cambios realizados por otros al origen de datos. Sin embargo, algunas características de la [el servicio de cursores de Microsoft para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), como eliminar la asociación<br /><br /> [Conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos, no se pueden simular con cursores de servidor y estas características estarán disponibles con esta opción.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
