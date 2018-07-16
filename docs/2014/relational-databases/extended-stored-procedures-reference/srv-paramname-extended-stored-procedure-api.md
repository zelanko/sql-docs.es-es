---
title: srv_paramname (API de procedimiento almacenado extendido) | Microsoft Docs
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
- srv_paramname
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_paramname
ms.assetid: 1a53d707-7b06-49cc-a0df-ac727cfe953f
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8108cbf1c08f9259734280105df931dc3f91203a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37217275"
---
# <a name="srvparamname-extended-stored-procedure-api"></a>srv_paramname (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Devuelve el nombre de un parámetro de llamada a un procedimiento almacenado remoto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBCHAR * srv_paramname (  
SRV_PROC * srvproc,intn, int *len );  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la llamada al procedimiento almacenado remoto). La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *n*  
 Indica el número del parámetro. El primer parámetro es 1.  
  
 *len*  
 Proporciona un puntero a una variable `int` que contiene la longitud (en bytes) del nombre de parámetro. Si *len* es NULL, no se devuelve la longitud del nombre de parámetro del procedimiento almacenado remoto.  
  
## <a name="returns"></a>Devuelve  
 Un puntero a una cadena de caracteres terminada en NULL que contiene el nombre del parámetro. La longitud del nombre de parámetro se almacena en *len*. Si no hay ningún parámetro *n* ni ningún procedimiento almacenado remoto, devuelve NULL, *len* se establece en -1 y se envía un mensaje de error informativo. Si el nombre de parámetro es NULL, *len* se establece en 0 y se devuelve una cadena vacía terminada en NULL.  
  
## <a name="remarks"></a>Notas  
 Esta función obtiene el nombre de un parámetro de llamada a un procedimiento almacenado remoto. Cuando se usan parámetros en una llamada a un procedimiento almacenado remoto, estos pueden pasarse por nombre o por posición (sin nombre). Se produce un error si la llamada al procedimiento almacenado remoto se realiza con algunos parámetros pasados por nombre y otros pasados por posición. Sigue llamándose al controlador SRV_RPC, pero parece como si no hubiera ningún parámetro y **srv_rpcparams** devuelve 0.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [srv_rpcparams &#40;API de procedimiento almacenado extendido&#41;](srv-rpcparams-extended-stored-procedure-api.md)  
  
  
