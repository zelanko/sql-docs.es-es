---
title: Propiedad SQLState | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 00ab80a10b2c7c411cee0fb6061467d67cfbd4a2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740365"
---
# <a name="sqlstate-property"></a>Propiedad SQLState
Indica el estado SQL para un determinado [Error](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve los cinco caracteres **cadena** valor que sigue el estándar ANSI SQL e indica el código de error.  
  
## <a name="remarks"></a>Comentarios  
 Use la **SQLState** propiedad para leer el código de error de cinco caracteres que devuelve el proveedor cuando se produce un error durante el procesamiento de una instrucción SQL. Por ejemplo, cuando se usa el proveedor Microsoft OLE DB para ODBC con una base de datos de Microsoft SQL Server, los códigos de error de estado SQL se originan en ODBC, basándose en los errores específicos de ODBC o sobre los errores que se originan en Microsoft SQL Server y, a continuación, se asignan a ODBC errores. Estos códigos de error se documentan en el estándar ANSI SQL, pero se pueden implementar de forma diferente por diferentes orígenes de datos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
