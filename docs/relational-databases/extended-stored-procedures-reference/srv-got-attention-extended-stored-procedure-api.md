---
title: srv_got_attention (API de procedimiento almacenado extendido) | Microsoft Docs
description: Obtenga información sobre cómo srv_got_attention comprueba si es necesario anular la conexión o la tarea actual y devuelve TRUE si la conexión se ha eliminado o se ha anulado el lote.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_got_attention
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_got_attention
ms.assetid: 805e68e1-d17f-41bd-8b9f-a27283bb6fbe
author: rothja
ms.author: jroth
ms.openlocfilehash: 2b5ba738ddd220d83cffe2c28b5629ee491d293f
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248453"
---
# <a name="srv_got_attention-extended-stored-procedure-api"></a>srv_got_attention (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Comprueba si es necesario anular la conexión o tarea actual y devuelve TRUE si se cancela la conexión o se anula el lote.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL srv_got_attention (SRV_PROC *   
srvproc  
);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *srvproc*  
 Puntero que identifica una conexión a la base de datos.  
  
## <a name="return-value"></a>Valor devuelto  
 TRUE si se cancela la conexión o se anula el lote. FALSE si la conexión o el lote están activos.  
  
## <a name="remarks"></a>Observaciones  
 Un procedimiento almacenado extendido de ejecución prolongada debe comprobar la atención del servidor al llamar periódicamente a **srv_got_attention** para que el procedimiento termine automáticamente cuando se cancele la conexión o se anule el lote.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
