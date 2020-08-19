---
description: Propiedad Source (Error de ADO)
title: Propiedad Source (error de ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fa7fc5c5098b6e429960e5d72702111abab55ac2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442057"
---
# <a name="source-property-ado-error"></a>Propiedad Source (Error de ADO)
Indica el nombre del objeto o la aplicación que originalmente generó un error.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **cadena** que indica el nombre de un objeto o una aplicación.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **source** en un objeto de [error](../../../ado/reference/ado-api/error-object.md) para determinar el nombre del objeto o la aplicación que originalmente generó un error. Podría ser el nombre de clase del objeto o el identificador de programación. En el caso de los errores de ADO, el valor de la propiedad será **ADODB.** _Objectname_, donde *objectname* es el nombre del objeto que desencadenó el error. Para ADOX y ADO MD, el valor será **ADOX.** _Objectname_ y **ADOMD.** _Objectname_, respectivamente.  
  
 En función de la documentación del error de las propiedades **source**, [Number](../../../ado/reference/ado-api/number-property-ado.md)y [Description](../../../ado/reference/ado-api/description-property.md) de los objetos de **error** , puede escribir código que controle el error de forma adecuada.  
  
 La propiedad de **origen** es de solo lectura para los objetos de **error** .  
  
## <a name="applies-to"></a>Se aplica a  
 [Error (objeto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propiedad Description](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, propiedades de HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propiedad Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propiedad Source (registro de ADO)](../../../ado/reference/ado-api/source-property-ado-record.md)   
 [Propiedad Source (ADO Recordset)](../../../ado/reference/ado-api/source-property-ado-recordset.md)
