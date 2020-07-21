---
title: Propiedad NativeError (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b9bd2228b38af302d96cd3794cc00674449fcac
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762406"
---
# <a name="nativeerror-property-ado"></a>Propiedad NativeError (ADO)
Indica el código de error específico del proveedor para un objeto de [error](../../../ado/reference/ado-api/error-object.md) determinado.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **tipo Long** que indica el código de error.  
  
## <a name="remarks"></a>Observaciones  
 Utilice la propiedad **NativeError** para recuperar la información de error específica de la base de datos para un objeto de **error** determinado. Por ejemplo, al usar el proveedor ODBC de Microsoft para OLE DB con una base de datos de Microsoft SQL Server, los códigos de error nativos que se originan a partir de SQL Server pasan a través de ODBC y el proveedor ODBC a la propiedad **NativeError** de ADO.  
  
## <a name="applies-to"></a>Se aplica a  
 [Error (objeto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
