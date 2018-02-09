---
title: srv_rpcoptions (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- srv_rpcoptions
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 151157986bee12807eccf4919248fbeb7dbcc29a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="srvrpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, use la integración de CLR.  
  
 Devuelve las opciones de tiempo de ejecución para el procedimiento almacenado remoto actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió el procedimiento almacenado remoto). La estructura contiene información que la biblioteca de API Procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
## <a name="returns"></a>Devuelve  
 Un mapa de bits que contiene las marcas en tiempo de ejecución combinadas en un OR lógico para el procedimiento almacenado remoto actual. Si no hay un procedimiento almacenado remoto actual, se devuelve 0 y se genera un mensaje.  
  
## <a name="remarks"></a>Comentarios  
 En la tabla siguiente se describen las marcas de tiempo de ejecución.  
  
|Marca de tiempo de ejecución|Description|  
|--------------------|-----------------|  
|SRV_NOMETADATA|El cliente ha solicitado resultados sin información de metadatos. Esta marca solamente se usa cuando el cliente se está comunicando con una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una aplicación API de procedimiento almacenado extendido no puede omitir información de metadatos.|  
|SRV_RECOMPILE|El cliente ha solicitado volver a compilar el procedimiento almacenado remoto antes de ejecutarlo. Esta marca no se puede aplicar a una aplicación API de procedimiento almacenado extendido.|  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
