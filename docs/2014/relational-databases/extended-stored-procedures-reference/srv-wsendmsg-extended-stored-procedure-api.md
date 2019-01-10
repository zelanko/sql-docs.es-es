---
title: srv_wsendmsg (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_wsendmsg
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 18b166472cff011b3766645dde61f562c766ff2c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366197"
---
# <a name="srvwsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg (API de procedimiento almacenado extendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Envía un mensaje Unicode al cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *Msgnum*  
 Es un número de mensaje de 4 bytes.  
  
 *Severity*  
 Especifica la gravedad del error. Una gravedad menor o igual que 10 se considera un mensaje informativo; de lo contrario, se considera un error.  
  
 *message*  
 Es un puntero a una cadena Unicode que se va a enviar al cliente.  
  
 *msglen*  
 Especifica la longitud en caracteres de *message*.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Utilice esta función para enviar mensajes en Unicode. Es similar a **srv_sendmsg**, pero el mensaje que envía es una cadena WCHAR en lugar de una cadena de tipo DBCHAR. Tenga en cuenta que la longitud del mensaje se indica en caracteres en lugar de en bytes y que *msglen* nunca será igual a SRV_NULLTERM.  
  
 La función devuelve FAIL cuando  
  
-   El argumento *msglen* proporcionado no está comprendido en el intervalo de 0 a 32242.  
  
-   El argumento *msglen* proporcionado es 0 pero el puntero del mensaje es NULL.  
  
-   Se produce un error al enviar el mensaje de error a través de la red.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Vea también  
 [srv_sendmsg &#40;API de procedimiento almacenado extendido&#41;](srv-sendmsg-extended-stored-procedure-api.md)  
  
  
