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
ms.openlocfilehash: 729675f7df3a4e394bb28f4074644289489ef248
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050797"
---
# <a name="srv_alloc-extended-stored-procedure-api"></a>srv_alloc (API de procedimiento almacenado extendido)
    
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
  
## <a name="returns"></a>Devoluciones  
 Un puntero al el espacio asignado más reciente. Si no se pueden asignar *size* bytes, se devuelve un puntero nulo.  
  
## <a name="remarks"></a>Comentarios  
 La función **srv_alloc** es equivalente a la función **GlobalAlloc** de la API de [!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows. Las funciones normales de administración de memoria en tiempo de ejecución de la API de Windows C, se pueden usar en una aplicación API de procedimiento almacenado extendido.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
