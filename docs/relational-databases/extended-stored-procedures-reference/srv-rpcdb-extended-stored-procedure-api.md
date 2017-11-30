---
title: srv_rpcdb (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: srv_rpcdb
apilocation: opends60.dll
apitype: DLLExport
dev_langs: C++
helpviewer_keywords: srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5228cb286ff9862568b05275d9ab499fe152f924
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="srvrpcdb-extended-stored-procedure-api"></a>srv_rpcdb (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve el componente nombre de base de datos del procedimiento almacenado remoto actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *len*  
 Es un puntero a una variable **int** que recibe la longitud del nombre de la base de datos. Si *len* es NULL, no se devuelve la longitud del nombre de la base de datos.  
  
## <a name="returns"></a>Devuelve  
 Un puntero DBCHAR a la cadena terminada en NULL para la parte de nombre de base de datos del procedimiento almacenado remoto actual. Si no hay ningún procedimiento almacenado remoto actual, se devuelve NULL y el parámetro *len* se establece en -1.  
  
## <a name="remarks"></a>Comentarios  
 Esta función devuelve solamente el componente de base de datos del nombre de objeto del procedimiento almacenado remoto. No incluye los especificadores opcionales para propietario, nombre de procedimiento almacenado remoto y número de procedimiento almacenado remoto.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
