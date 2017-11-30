---
title: srv_rpcname (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_rpcname
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ef17597c30245cf1655dfbdac94dd7884914026c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="srvrpcname-extended-stored-procedure-api"></a>srv_rpcname (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve el componente nombre de procedimiento del procedimiento almacenado remoto actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBCHAR * srv_rpcname (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió el procedimiento almacenado remoto). La estructura contiene información que la biblioteca de API Procedimiento almacenado extendido utiliza para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *len*  
 Es un puntero a una variable entera que recibe la longitud del nombre de la base de datos. Si *len* es NULL, no se devuelve la longitud del nombre del procedimiento almacenado remoto.  
  
## <a name="returns"></a>Devuelve  
 Un puntero DBCHAR a la cadena terminada en NULL para el componente nombre de procedimiento almacenado remoto del procedimiento almacenado remoto actual. Si no hay ningún procedimiento almacenado remoto actual, se devuelve NULL y *len* se establece en -1.  
  
## <a name="remarks"></a>Comentarios  
 Esta función solo devuelve el nombre del procedimiento almacenado remoto. No incluye los especificadores opcionales propietario, nombre de la base de datos y número de procedimiento almacenado remoto.  
  
 Puesto que es válido llamar a **srv_rpcname** cuando no es un procedimiento almacenado remoto (no se produce ningún error informativo), esta función proporciona un método para determinar si existe un procedimiento almacenado remoto.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
