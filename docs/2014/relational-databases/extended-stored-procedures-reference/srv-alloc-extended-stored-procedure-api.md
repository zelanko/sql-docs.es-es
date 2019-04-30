---
title: srv_alloc (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_alloc
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 61157ab8ba2b9f47caf89b6a16a3edd830437abf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138912"
---
# <a name="srvalloc-extended-stored-procedure-api"></a>srv_alloc (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Asigna la memoria de forma dinámica.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *size*  
 Especifica el número de bytes para asignar.  
  
## <a name="returns"></a>Devuelve  
 Un puntero al el espacio asignado más reciente. Si no se pueden asignar *size* bytes, se devuelve un puntero nulo.  
  
## <a name="remarks"></a>Comentarios  
 La función **srv_alloc** es equivalente a la función **GlobalAlloc** de la API de [!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows. Las funciones normales de administración de memoria en tiempo de ejecución de la API de Windows C, se pueden usar en una aplicación API de procedimiento almacenado extendido.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
  
