---
title: bcp_done | Documentos de Microsoft
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
- bcp_done
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_done function
ms.assetid: e59b3f16-5b59-40da-880f-f3edf657d1ee
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 56c1d20d56d95263e93e33a45f712447b749b1be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204392"
---
# <a name="bcpdone"></a>bcp_done
  Finaliza una copia masiva de las variables de programa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizada con [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBINT bcp_done (  
    HDBC   
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
## <a name="returns"></a>Devuelve  
 El número de filas guardado permanentemente después de la última llamada a [bcp_batch](bcp-batch.md) , o-1 en caso de error.  
  
## <a name="remarks"></a>Notas  
 Llame a **bcp_done** después de la última llamada a [bcp_sendrow](bcp-sendrow.md) o [bcp_moretext](bcp-moretext.md). Si no se llama a **a bcp_done** después de copiar todos los datos se producen errores.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  