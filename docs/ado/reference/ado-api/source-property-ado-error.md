---
title: Origen (propiedad, ADO Error) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63407f75c5bee03d24b5b3f69c2ef94cb38e177e
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168725"
---
# <a name="source-property-ado-error"></a>Propiedad Source (Error de ADO)
Indica el nombre del objeto o la aplicación que ha generado un error.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **cadena** valor que indica el nombre de un objeto o la aplicación.  
  
## <a name="remarks"></a>Comentarios  
 Use la **origen** propiedad en un [Error](../../../ado/reference/ado-api/error-object.md) objeto para determinar el nombre del objeto o la aplicación que ha generado un error. Esto podría ser el nombre de clase o el ID del objeto Para los errores de ADO, será el valor de propiedad **ADODB.** _ObjectName_, donde *ObjectName* es el nombre del objeto que desencadenó el error. En ADOX y ADO MD, el valor será **ADOX.** _ObjectName_ y **ADOMD.** _ObjectName_, respectivamente.  
  
 Basándose en la documentación de error desde el **origen**, [número](../../../ado/reference/ado-api/number-property-ado.md), y [descripción](../../../ado/reference/ado-api/description-property.md) propiedades de **Error** objetos, puede escribir código que va a controlar el error adecuadamente.  
  
 El **origen** propiedad es de solo lectura para **Error** objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propiedad Description](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, HelpFile propiedades](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propiedad Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propiedad Source (Record ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
