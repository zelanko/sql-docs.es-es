---
title: srv_senddone (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- srv_senddone
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_senddone
ms.assetid: 1fc4f1d5-56d4-43f6-b5e4-0c0cc295cba3
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6a7ed324a068b81c2226a0b520d403f688a6ede7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108964"
---
# <a name="srvsenddone-extended-stored-procedure-api"></a>srv_senddone (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Envía un mensaje de finalización del resultado al cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_senddone (  
SRV_PROC *  
srvproc  
,  
DBUSMALLINT   
status  
,  
DBUSMALLINT  
info  
,  
DBINT  
count   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la solicitud de idioma). La estructura contiene información que la biblioteca de API Procedimiento almacenado extendido utiliza para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *status*  
 Es un campo de 2 bytes para varias marcas *status* . Varias marcas se pueden establecer mediante los operadores lógicos AND y OR con valores de marca *status* . En la tabla siguiente se enumeran las marcas posibles *status* .  
  
|Marca de estado|Descripción|  
|-----------------|-----------------|  
|SRV_DONE_COUNT|El parámetro *count* contiene un recuento válido.|  
|SRV_DONE_ERROR|El comando de cliente actual recibió un error.|  
  
 *info*  
 Es un campo reservado de 2 bytes. Establezca este valor en 0.  
  
 *Recuento*  
 Es un campo de 4 bytes que se usa para indicar un recuento para el conjunto de resultados actual. Si la marca SRV_DONE_COUNT se establece en el campo *status* , *count* contiene un recuento válido.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL  
  
## <a name="remarks"></a>Notas  
 Una solicitud de cliente puede ocasionar que el servidor ejecute varios comandos y que devuelva varios conjuntos de resultados. Para cada conjunto de resultados, **srv_senddone** debe devolver un mensaje de finalización del resultado al cliente.  
  
 El campo *count* indica el número de filas afectadas por un comando. Si el campo *count* contiene un recuento, la marca SRV_DONE_COUNT se debería establecer en el campo *status* . Este valor permite al cliente distinguir entre un valor *count* de 0 y un campo *count* no usado.  
  
 No llame a **srv_senddone** desde el controlador SRV_CONNECT.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  