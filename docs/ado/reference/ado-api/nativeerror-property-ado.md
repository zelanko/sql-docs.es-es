---
title: Propiedad NativeError (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 94a6b8f28a80202f293008c16f40c0eed0730996
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="nativeerror-property-ado"></a>Propiedad NativeError (ADO)
Indica el código de error específico del proveedor para un determinado [Error](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un **largo** valor que indica el código de error.  
  
## <a name="remarks"></a>Comentarios  
 Use la **NativeError** propiedad que se va a recuperar la información de error específico de la base de datos para un determinado **Error** objeto. Por ejemplo, al usar el proveedor ODBC de Microsoft para OLE DB con una base de datos de Microsoft SQL Server, códigos de error nativos que se originan en SQL Server pasan a través de ODBC y el proveedor ODBC a ADO **NativeError** propiedad.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   

