---
title: FrameWindowVisible | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 9091d714-98bc-43ec-b8d1-9c892cb57f19
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f09e83d79a913bb56042a5a48b832a940e0f9ea9
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sqltoolsvsnativehelpers---framewindowvisible"></a>SqlToolsVSNativeHelpers - FrameWindowVisible
  Propiedad que especifica si un marco de ventana proporcionado es visible. El método auxiliar se utiliza a partir del código administrado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL WINAPI IsFrameWindowVisible(IVsWindowFrame* frame)  
{  
    if (NULL == frame)  
    {  
        return FALSE;  
    }  
  
    return S_OK == frame->IsVisible();  
}  
```  
  
#### <a name="parameters"></a>Parámetros  
 *frame*  
  
 Puntero de IVsWindowFrame* a Visual Studio WindowFrame.  
  
## <a name="property-valuereturn-value"></a>Valor de propiedad/Valor devuelto  
 Valor booleano que especifica si el marco de la ventana especificada por *frame* está visible.  
  
## <a name="see-also"></a>Vea también  
 [SqlToolsVSNativeHelpers](../relational-databases/sqltoolsvsnativehelpers.md)  
  
  
