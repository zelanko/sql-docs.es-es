---
title: Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apilocation:
- SSTRANSTIGHTLYCPLD Field (SQLServerXAResource)
apitype: Assembly
ms.assetid: 379857c3-9de1-4964-8782-32df317cbfbb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8129cf30a7ba95c39281c9ff4bd2a5c0eac4183c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818423"
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se utiliza para permitir transacciones XA estrechamente acopladas, las cuales tienen identificadores de rama de transacción XA diferentes (XID), pero tienen el mismo identificador de transacción global (GTRID).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>Valor de campo  
 Un **int** valor de 32768.  
  
## <a name="remarks"></a>Notas  
 Cada transacción queda identificada por un identificador de rama de transacción XA (XID) y un identificador de transacción global (GTRID). Para permitir que las aplicaciones utilicen transacciones XA estrechamente acopladas con XID diferentes pero con el mismo GTRID, debe establecer [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) en el parámetro flags del método XAResource.start. Para obtener más información sobre cómo usar esta marca, vea [descripción de las transacciones XA](../../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Ver también  
 [Campos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [Miembros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
