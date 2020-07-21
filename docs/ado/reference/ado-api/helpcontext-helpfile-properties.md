---
title: Propiedades HelpContext y HelpFile | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
author: rothja
ms.author: jroth
ms.openlocfilehash: 13fb3f0b5bf55ac9acb525183eba6d8645f4de62
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758721"
---
# <a name="helpcontext-helpfile-properties"></a>HelpContext, HelpFile propiedades
Indica el archivo de ayuda y el tema asociados a un objeto de [error](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-values"></a>Valores devueltos  
  
-   **HelpContextID** Devuelve un identificador de contexto, como un valor **largo** , para un tema en un archivo de ayuda.  
  
-   **ArchivoDeAyuda** Devuelve un valor de **cadena** que se evalúa como una ruta de acceso totalmente resuelta a un archivo de ayuda.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica un archivo de ayuda en la propiedad **HelpFile** , la propiedad **HelpContext** se usa para mostrar automáticamente el tema de ayuda que identifica. Si no hay ningún tema de ayuda relevante disponible, la propiedad **HelpContext** devuelve cero y la propiedad **HelpFile** devuelve una cadena de longitud cero ("").  
  
## <a name="applies-to"></a>Se aplica a  
 [Error (objeto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Propiedad Description](../../../ado/reference/ado-api/description-property.md)   
 [Propiedad Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propiedad Source (Error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
