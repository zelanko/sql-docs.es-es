---
title: srv_sendmsg (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- srv_sendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_sendmsg
ms.assetid: efcb50b9-f8ff-4121-bf67-05830171b928
caps.latest.revision: 30
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fd9353044e5c6ab8edde8989cfb8eb0c663f29b8
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="srvsendmsg-extended-stored-procedure-api"></a>srv_sendmsg (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Envía un mensaje al cliente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_sendmsg (  
SRV_PROC *  
srvproc  
,  
int  
msgtype  
,  
DBINT  
msgnum  
,  
DBTINYINT  
class  
,   
DBTINYINT  
state  
,  
DBCHAR *  
rpcname  
,  
int   
rpcnamelen  
,  
DBUSMALLINT  
linenum  
,  
DBCHAR *  
message  
,  
int  
msglen   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC, que es el identificador de una conexión de cliente determinada (en este caso, el identificador que recibió la solicitud de idioma). La estructura contiene información que la biblioteca de API Procedimiento almacenado extendido utiliza para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *msgtype*  
 Es SRV_MSG_INFO o SRV_MSG_ERROR, dependiendo de si el servidor está enviando un mensaje informativo o de error.  
  
 *msgnum*  
 Es un número de mensaje de 4 bytes.  
  
 *class*  
 Especifica la gravedad del error. Una gravedad menor o igual a 10 se considera un mensaje informativo.  
  
 *state*  
 Proporciona el número de estado de error para el mensaje actual. El número de estado de error proporciona información sobre el contexto del error. Los números de estado van de 0 a 255.  
  
 *rpcname*  
 No se admite actualmente.  
  
 *rpcnamelen*  
 No se admite actualmente.  
  
 *linenum*  
 Es el número de línea en el lote de comandos del lenguaje donde se aplica el mensaje. Los números de línea empiezan por 1. Si *linenum* no se aplica al mensaje, se establece en 0.  
  
 *message*  
 Es un puntero a una cadena de caracteres que se va a enviar al cliente.  
  
 *msglen*  
 Especifica la longitud en bytes de *message*. Si *message* está terminado en null, establezca *msglen* en SRV_NULLTERM.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL  
  
## <a name="remarks"></a>Comentarios  
 Esta función envía mensajes de error o informativos al cliente. Se llama una vez por cada mensaje que se va a enviar.  
  
 Los mensajes se pueden enviar al cliente con **srv_sendmsg** en cualquier orden antes o después de haber enviado todas las filas (si las hubiera) con **srv_sendrow**. Todos los mensajes, si los hubiera, se deben enviar al cliente antes de enviar el estado de finalización con **srv_senddone**.  
  
 Para enviar mensajes en Unicode, use **srv_wsendmsg** en lugar de **srv_sendmsg**.  
  
 Para más información, vea [Datos Unicode y páginas de códigos de servidor](../../relational-databases/extended-stored-procedures-programming/unicode-data-and-server-code-pages.md).  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](http://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409http://msdn.microsoft.com/security/).  
  
  
