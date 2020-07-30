---
title: srv_rpcparams (API de procedimiento almacenado extendido) | Microsoft Docs
description: Obtenga información sobre srv_rpcparams y cómo puede devolver el número de parámetros para el procedimiento almacenado remoto actual.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcparams
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcparams
ms.assetid: 96a5e6f6-d320-4623-b96e-0a856e3abebb
author: rothja
ms.author: jroth
ms.openlocfilehash: 47fa4b7a539f1491d539b73fdcc50a9b298db910
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248264"
---
# <a name="srv_rpcparams-extended-stored-procedure-api"></a>srv_rpcparams (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve el número de parámetros del procedimiento almacenado remoto actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_rpcparams ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió el procedimiento almacenado remoto). La estructura contiene información que la biblioteca de API Procedimiento almacenado extendido utiliza para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
## <a name="returns"></a>Devuelve  
 El número de parámetros en el procedimiento almacenado remoto. Si no hay ningún parámetro en el procedimiento almacenado remoto o si no hay un procedimiento almacenado remoto actual, se devuelve -1 y se produce un error de la información.  
  
## <a name="remarks"></a>Observaciones  
 Esta función devuelve el número de parámetros en el procedimiento almacenado remoto el actual. Normalmente se realiza la llamada desde el procedimiento almacenado remoto.  
  
 Cuando se usan parámetros en una llamada a un procedimiento almacenado remoto, estos pueden pasarse por nombre o por posición (sin nombre). Se producirá un error en la llamada al procedimiento almacenado remoto si algunos parámetros se pasan por nombre y otros por posición. Cuando se produce este error, se llama al controlador del procedimiento almacenado remoto, pero no recibe los parámetros y **srv_rpcparams** devuelve 0.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
