---
title: CursorLocationEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CursorLocationEnum
helpviewer_keywords:
- CursorLocationEnum enumeration [ADO]
ms.assetid: acb255ff-1734-4b70-89bb-aef862b4c63b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 832372ee3f8e80a9da4a758c759d9b5399a20a57
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614739"
---
# <a name="cursorlocationenum"></a>CursorLocationEnum
Especifica la ubicación del servicio de cursor.  
  
|Constante|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**adUseClient**|3|Utiliza cursores de cliente proporcionados por una biblioteca de cursores locales. Servicios de cursores locales a menudo le permitirá muchas características proporcionado por el controlador de cursores no pueden, por lo que esta configuración puede proporcionar una ventaja con respecto a las características que se habilitarán. Por compatibilidad con versiones anteriores, el sinónimo **adUseClientBatch** también es compatible.|  
|**adUseNone**|1|No utiliza servicios de cursor. (Esta constante es obsoleta y aparece únicamente por motivos de compatibilidad con versiones anteriores).|  
|**adUseServer**|2|Predeterminado: Utiliza cursores proporcionados por el proveedor de datos o el controlador. Estos cursores a veces son muy flexibles y permiten una sensibilidad adicional a otros cambios en el origen de datos. Sin embargo, algunas características de la [el servicio de cursores de Microsoft para OLE DB](../../../ado/guide/data/the-microsoft-cursor-service-for-ole-db.md), como eliminar la asociación<br /><br /> [Conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) objetos, no se pueden simular con cursores de servidor y estas características dejarán de estar disponibles con esta configuración.|  
  
## <a name="adowfc-equivalent"></a>Equivalente de ADO y WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.CursorLocation.CLIENT|  
|AdoEnums.CursorLocation.NONE|  
|AdoEnums.CursorLocation.SERVER|  
  
## <a name="applies-to"></a>Se aplica a  
 [Propiedad CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)
