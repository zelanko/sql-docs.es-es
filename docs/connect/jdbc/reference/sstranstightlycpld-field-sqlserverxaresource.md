---
title: Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8323c328938188b16d56f9dfa05c3dfd2be16c75
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32848050"
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se utiliza para permitir transacciones XA estrechamente acopladas, las cuales tienen identificadores de rama de transacción XA diferentes (XID), pero tienen el mismo identificador de transacción global (GTRID).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>Valor de campo  
 Un **int** valo 32768.  
  
## <a name="remarks"></a>Comentarios  
 Cada transacción queda identificada por un identificador de rama de transacción XA (XID) y un identificador de transacción global (GTRID). Para permitir que las aplicaciones usen transacciones XA estrechamente acopladas con XID diferentes pero tener el mismo GTRID, debe establecer el [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) en el parámetro flags del método XAResource.start. Para obtener más información sobre cómo usar esta marca, consulte [descripción de las transacciones XA](../../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Vea también  
 [Campos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [Miembros de SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
