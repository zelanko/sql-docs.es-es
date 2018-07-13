---
title: srv_got_attention (API de procedimiento almacenado extendido) | Microsoft Docs
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
- srv_got_attention
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d7d6f026b9c851c7fb8636442cfda27a870be861
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37201405"
---
# <a name="srvgotattention-extended-stored-procedure-api"></a>srv_got_attention (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Comprueba si es necesario anular la conexión o tarea actual y devuelve TRUE si se cancela la conexión o se anula el lote.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL srv_got_attention  
(SRV_PROC *  
srvproc  
);  
  
```  
  
#### <a name="parameters"></a>Parámetros  
 *srvproc*  
 Puntero que identifica una conexión a la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 TRUE si se cancela la conexión o se anula el lote. FALSE si la conexión o el lote están activos.  
  
## <a name="remarks"></a>Notas  
 Un procedimiento almacenado extendido de ejecución prolongada debe comprobar la atención del servidor al llamar periódicamente a **srv_got_attention** para que el procedimiento termine automáticamente cuando se cancele la conexión o se anule el lote.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
