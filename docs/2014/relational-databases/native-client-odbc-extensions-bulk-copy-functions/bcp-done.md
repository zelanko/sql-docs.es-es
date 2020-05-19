---
title: bcp_done | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ca26e8e8f3bdb17afe9908b99bfe5cf09ff3b563
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82701985"
---
# <a name="bcp_done"></a>bcp_done
  Finaliza una copia masiva de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizada con [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
## <a name="returns"></a>Devoluciones  
 El número de filas guardado permanentemente después de la última llamada a [bcp_batch](bcp-batch.md) , o-1 en caso de error.  
  
## <a name="remarks"></a>Observaciones  
 Llame a **bcp_done** después de la última llamada a [bcp_sendrow](bcp-sendrow.md) o [bcp_moretext](bcp-moretext.md). Si no se llama a **a bcp_done** después de copiar todos los datos se producen errores.  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
