---
title: 'Propiedad prompt: dinámica (ADO) | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67931572"
---
# <a name="prompt-property-dynamic-ado"></a>Propiedad-dinámica Prompt (ADO)
Especifica si el proveedor de OLE DB debe solicitar al usuario la información de inicialización.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un valor de [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) .  
  
## <a name="remarks"></a>Observaciones  
 **Prompt** es una propiedad dinámica que el proveedor de OLE DB puede anexar a la colección de [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) del objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) . Para solicitar información de inicialización, los proveedores de OLE DB normalmente mostrarán un cuadro de diálogo al usuario.  
  
 Las propiedades dinámicas de un objeto de [conexión](../../../ado/reference/ado-api/connection-object-ado.md) se pierden cuando se cierra la **conexión** . La propiedad **prompt** debe restablecerse antes de volver a abrir la **conexión** para usar un valor distinto del predeterminado.  
  
> [!NOTE]
>  No especifique que el proveedor debe preguntar al usuario en los escenarios en los que el usuario no podrá responder al cuadro de diálogo. Por ejemplo, el usuario no podrá responder si la aplicación se ejecuta en un sistema de servidor en lugar de en el cliente del usuario, o si la aplicación se está ejecutando en un sistema sin ningún usuario que haya iniciado sesión. En estos casos, la aplicación espera indefinidamente una respuesta y parece que se bloquea.  
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
