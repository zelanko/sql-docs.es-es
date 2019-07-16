---
title: (ADO) propiedad-dinámica Prompt | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cde7a5ad0324bc7d5cde5e1a794eeb9e2cb3381a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931572"
---
# <a name="prompt-property-dynamic-ado"></a>Propiedad-dinámica Prompt (ADO)
Especifica si el proveedor OLE DB debe solicitar al usuario información de inicialización.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) valor.  
  
## <a name="remarks"></a>Comentarios  
 **Símbolo del sistema** es una propiedad dinámica que se puede anexar a la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección por el proveedor OLE DB. Para solicitar información de inicialización, los proveedores OLE DB normalmente mostrará un cuadro de diálogo al usuario.  
  
 Propiedades dinámicas de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto se perderán cuando el **conexión** está cerrado. El **Prompt** propiedad se debe restablecer antes de volver a abrir el **conexión** para utilizar un valor distinto del predeterminado.  
  
> [!NOTE]
>  No se especifica que el proveedor debe solicitar al usuario en escenarios en los que el usuario no pueda responder al cuadro de diálogo. Por ejemplo, el usuario no podrá responder si la aplicación se ejecuta en un sistema de servidor en lugar de en el cliente del usuario, o si la aplicación se ejecuta en un sistema con ningún usuario inicie sesión. En estos casos, la aplicación se espere indefinidamente una respuesta y se parece al bloqueo.  
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
