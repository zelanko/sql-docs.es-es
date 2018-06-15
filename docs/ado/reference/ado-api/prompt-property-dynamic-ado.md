---
title: Solicitar propiedad dinámicos (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Prompt property [ADO]
ms.assetid: c4f001b5-8d16-4d39-a42e-c0e2faaaceaf
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7b5c0637f7befb1419f5cb96bbcd421d59cc7b8
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35280637"
---
# <a name="prompt-property-dynamic-ado"></a>Propiedad-dinámica Prompt (ADO)
Especifica si el proveedor OLE DB debe solicitar al usuario información de inicialización.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece y devuelve un [ConnectPromptEnum](../../../ado/reference/ado-api/connectpromptenum.md) valor.  
  
## <a name="remarks"></a>Notas  
 **Símbolo del sistema** es una propiedad dinámica, que puede ser anexada a la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) del objeto [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección por el proveedor OLE DB. Para solicitar información de inicialización, los proveedores OLE DB normalmente mostrará un cuadro de diálogo al usuario.  
  
 Propiedades dinámicas de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto se pierden cuando el **conexión** está cerrado. El **Prompt** propiedad se debe restablecer antes de volver a abrir la **conexión** para utilizar un valor distinto del predeterminado.  
  
> [!NOTE]
>  No especifique que el proveedor debe preguntar al usuario en escenarios en los que el usuario no pueda responder al cuadro de diálogo. Por ejemplo, el usuario no podrá responder si la aplicación se ejecuta en un sistema de servidor en lugar de en el cliente del usuario, o si la aplicación se ejecuta en un sistema con ningún usuario ha iniciado sesión. En estos casos, la aplicación se espere indefinidamente una respuesta y se parece al bloqueo.  
  
## <a name="usage"></a>Uso  
  
```  
Set cn = New Connection  
cn.Provider = "SQLOLEDB"  
cn.Properties("Prompt") = adPromptNever    ' do not prompt the user  
```  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
