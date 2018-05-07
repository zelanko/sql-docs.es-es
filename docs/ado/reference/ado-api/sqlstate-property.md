---
title: La propiedad SQLState | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetSQLState
- Error::SQLState
- Error::get_SQLState
helpviewer_keywords:
- SQLState property
ms.assetid: f9e25967-54b0-444d-af2a-0d2c75365d3e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ddc3d1e21bd4ba860dbb00e814518b658a9aa11e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlstate-property"></a>Propiedad SQLState
Indica el estado SQL para un determinado [Error](../../../ado/reference/ado-api/error-object.md) objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un carácter de cinco **cadena** valor que sigue el estándar ANSI SQL e indica el código de error.  
  
## <a name="remarks"></a>Comentarios  
 Use la **SQLState** propiedad que se va a leer el código de error de cinco caracteres que devuelve el proveedor cuando se produce un error durante el procesamiento de una instrucción SQL. Por ejemplo, cuando se utiliza el proveedor Microsoft OLE DB para ODBC con una base de datos de Microsoft SQL Server, códigos de error de estado SQL se originan en ODBC, basándose en errores específicos de ODBC o sobre los errores que se originan en Microsoft SQL Server y, a continuación, se asignan a ODBC errores. Estos códigos de error están documentados en el estándar ANSI SQL, pero pueden implementarse de forma diferente por diferentes orígenes de datos.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vea también  
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Descripción, HelpContext, HelpFile, NativeError, número, origen y ejemplo de las propiedades SQLState (VC ++)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
