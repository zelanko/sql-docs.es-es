---
title: Source (propiedad) (Error de ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords: Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a0f34bfbe5c4d7fa251316658dd76878c7b53c5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="source-property-ado-error"></a>Propiedad Source (Error de ADO)
Indica el nombre del objeto o la aplicación que ha generado un error.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **cadena** valor que indica el nombre de un objeto o la aplicación.  
  
## <a name="remarks"></a>Comentarios  
 Use la **origen** propiedad en un [Error](../../../ado/reference/ado-api/error-object.md) objeto para determinar el nombre del objeto o la aplicación que ha generado un error. Esto podría ser el nombre de clase del objeto o identificador de programación. Si hay errores en ADO, el valor de propiedad será **ADODB.** *ObjectName*, donde *ObjectName* es el nombre del objeto que desencadenó el error. En ADOX y ADO MD, el valor será **ADOX.** *ObjectName* y **ADOMD.** *ObjectName,* respectivamente.  
  
 Basándose en la documentación de error desde el **origen**, [número](../../../ado/reference/ado-api/number-property-ado.md), y [descripción](../../../ado/reference/ado-api/description-property.md) propiedades de **Error** objetos, puede escribir código el error que controlará adecuadamente.  
  
 El **origen** propiedad es de solo lectura para **Error** objetos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description (propiedad)](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, HelpFile propiedades](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propiedad Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propiedad Source (Record ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
