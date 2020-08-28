---
description: Propiedad Number (ADO)
title: Propiedad Number (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: rothja
ms.author: jroth
ms.openlocfilehash: a44c1a4902dbcd37089ee63c41db2b9a089c3aed
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990436"
---
# <a name="number-property-ado"></a>Propiedad Number (ADO)
Indica el número que identifica de forma única un objeto de [error](./error-object.md) .  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor **Long** que puede corresponder a una de las constantes [ErrorValueEnum](./errorvalueenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **Number** para determinar el error que se ha producido. El valor de la propiedad es un número único que corresponde a la condición de error.  
  
 La colección de [errores](./errors-collection-ado.md) devuelve un valor HRESULT en formato hexadecimal (por ejemplo, 0x80004005) o valor largo (por ejemplo, 2147467259). Estos valores HRESULT pueden ser generados por componentes subyacentes, como OLE DB o incluso OLE. Para obtener más información sobre estos números, vea [errores (OLE DB)](/previous-versions/windows/desktop/ms724533(v=vs.85)) en la [Referencia del programador de OLE DB](/previous-versions/windows/desktop/ms713643(v=vs.85))*.*  
  
## <a name="applies-to"></a>Se aplica a  
 [Error (objeto)](./error-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propiedad Description](./description-property.md)   
 [HelpContext, propiedades de HelpFile](./helpcontext-helpfile-properties.md)   
 [Propiedad Source (Error de ADO)](./source-property-ado-error.md)