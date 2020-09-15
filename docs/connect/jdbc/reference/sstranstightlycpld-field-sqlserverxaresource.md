---
description: Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3161ceb41586e330bee39206700702cf3d36239
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431557"
---
# <a name="sstranstightlycpld-field-sqlserverxaresource"></a>Campo SSTRANSTIGHTLYCPLD (SQLServerXAResource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se utiliza para permitir transacciones XA estrechamente acopladas, las cuales tienen identificadores de rama de transacción XA diferentes (XID), pero tienen el mismo identificador de transacción global (GTRID).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public static final int SSTRANSTIGHTLYCPLD  
```  
  
## <a name="field-value"></a>Valor de campo  
 Un valor **int** de 32768.  
  
## <a name="remarks"></a>Observaciones  
 Cada transacción queda identificada por un identificador de rama de transacción XA (XID) y un identificador de transacción global (GTRID). Para permitir que las aplicaciones utilicen transacciones XA estrechamente acopladas con XID diferentes pero con el mismo GTRID, debe establecer [SSTRANSTIGHTLYCPLD](../../../connect/jdbc/reference/sstranstightlycpld-field-sqlserverxaresource.md) en el parámetro flags del método XAResource.start. Para más información sobre cómo usar esta marca, vea [Descripción de las transacciones XA](../../../connect/jdbc/understanding-xa-transactions.md).  
  
## <a name="see-also"></a>Consulte también  
 [Campos SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-fields.md)   
 [Miembros SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-members.md)   
 [Clase SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md)  
  
  
