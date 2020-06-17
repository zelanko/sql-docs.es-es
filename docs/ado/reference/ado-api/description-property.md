---
title: Propiedad Description | Microsoft Docs
description: Obtenga información sobre la propiedad Description del objeto error en ADO que devuelve un valor de cadena que contiene una descripción del error.
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: rothja
ms.author: jroth
ms.openlocfilehash: 5bbaa998c419ba1a0af49ffa28e32fe91ffc96b9
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84880541"
---
# <a name="description-property"></a>Description (propiedad)
Describe un objeto de [error](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de **cadena** que contiene una descripción del error.  
  
## <a name="remarks"></a>Comentarios  
 Use la propiedad **Description** para obtener una descripción breve del error. Muestra esta propiedad para avisar al usuario de un error que no se puede o no desea controlar. La cadena procederá de ADO o de un proveedor.  
  
 Los proveedores son responsables de pasar texto de error específico a ADO. ADO agrega un objeto [error](../../../ado/reference/ado-api/error-object.md) a la colección de **errores** por cada error de proveedor o advertencia que recibe. Enumere la colección de **errores** para realizar un seguimiento de los errores que pasa el proveedor.  
  
## <a name="applies-to"></a>Se aplica a  
 [Error (objeto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Ejemplo de las propiedades Description, HelpContext, HelpFile, NativeError, Number, Source y SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext, propiedades de HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Propiedad Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Propiedad Source (Error de ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
