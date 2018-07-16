---
title: srv_alloc (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
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
caps.latest.revision: 32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5cc264f27814ed5d577dddfae5bc0d2cb81cc34
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236785"
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
  
## <a name="remarks"></a>Notas  
 La función **srv_alloc** es equivalente a la función **GlobalAlloc** de la API de [!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows. Las funciones normales de administración de memoria en tiempo de ejecución de la API de Windows C, se pueden usar en una aplicación API de procedimiento almacenado extendido.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
