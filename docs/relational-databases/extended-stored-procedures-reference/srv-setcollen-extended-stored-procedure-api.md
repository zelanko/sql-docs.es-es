---
title: srv_setcollen (API de procedimiento almacenado extendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setcollen
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setcollen
ms.assetid: 3c60f1c3-4562-463a-a259-12df172788bd
author: rothja
ms.author: jroth
ms.openlocfilehash: 15bd83b902ad64213fcde3ef15a185d69fde8cd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119639"
---
# <a name="srvsetcollen-extended-stored-procedure-api"></a>srv_setcollen (API de procedimiento almacenado extendido)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Especifica la longitud actual de los datos en bytes de una columna de longitud variable o de una columna que permite valores NULL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_setcollen (  
SRV_PROC *  
srvproc  
,  
int   
column  
,  
int  
len   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *column*  
 Indica el número de la columna para la que se especifica la longitud de datos. Las columnas se numeran comenzando por 1.  
  
 *len*  
 Indica la longitud, en bytes, de los datos de la columna. Una longitud de 0 indica que el valor de datos de la columna es NULL.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 Cada columna de la fila se debe definir antes con **srv_describe**. La longitud de datos de columna se establece mediante la última llamada a **srv_describe** o **srv_setcollen**. Si en una fila cambian los datos de longitud variable (datos terminados en NULL), se debe usar **srv_setcollen** para establecerlos en la nueva longitud antes de llamar a **srv_sendrow**. En una columna que permite valores NULL, es necesario llamar previamente a **srv_describe** con *desttype* establecido en un tipo de datos que permita valores NULL (como SRVINTN) y especificar datos NULL mediante una llamada a **srv_setcollen** con *len* establecido en 0. Los datos de longitud cero no se pueden especificar mediante la API Procedimiento almacenado extendido.  
  
 Tenga en cuenta que si el tipo de datos de la columna es de longitud variable, no se comprueba *len*. Esta función devuelve FAIL si se llama en una columna de longitud fija.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409 https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte también  
 [srv_describe &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
