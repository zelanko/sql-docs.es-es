---
title: srv_setutype (API de procedimiento almacenado extendido) | Microsoft Docs
description: Más información sobre srv_setutype. srv_setutype establece el tipo de datos definido por el usuario para una columna de una fila.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_setutype
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_setutype
ms.assetid: 6160f15d-1b68-411e-ab6d-491ec288f264
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ecdbaef663059146f3ca6bd4a88305e12d4f495
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248198"
---
# <a name="srv_setutype-extended-stored-procedure-api"></a>srv_setutype (API de procedimiento almacenado extendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Establece el tipo de datos definido por el usuario para una columna de una fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int srv_setutype (  
SRV_PROC *  
srvproc  
,  
int   
column  
,   
DBINT  
user_type   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 Es un puntero a la estructura SRV_PROC que es el identificador de una conexión cliente determinada. La estructura contiene información que la biblioteca de API de procedimiento almacenado extendido usa para administrar la comunicación y los datos entre la aplicación y el cliente.  
  
 *column*  
 Indica qué columna se va a establecer. Las columnas se numeran comenzando por 1.  
  
 *user_type*  
 Especifica el código del tipo de datos definido por el usuario.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL. Devuelve FAIL si la columna no existe.  
  
## <a name="remarks"></a>Observaciones  
 Una columna tiene dos tipos de datos: el tipo de datos real y el tipo de datos definido por el usuario. Usa el tipo de datos definido por el usuario [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para almacenar el tipo de datos definido por el usuario real de la columna, si existe, y la información de descripción de la columna, como la nulabilidad y la actualización, para la columna.  
  
 Se puede llamar a la función **srv_setutype** en cualquier momento siempre que se haya definido *column* con **srv_describe** y antes de que se haya enviado la última fila.  
  
> [!IMPORTANT]  
>  Debe revisar minuciosamente el código fuente de los procedimientos almacenados extendidos y debe probar las DLL compiladas antes de instalarlas en el servidor de producción. Para obtener información acerca de la revisión y pruebas de seguridad, vea este [sitio web de Microsoft](https://www.microsoft.com/msrc?rtc=1).  
  
## <a name="see-also"></a>Consulte también  
 [srv_describe &#40;API de procedimiento almacenado extendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-describe-extended-stored-procedure-api.md)  
  
  
