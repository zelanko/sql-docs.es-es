---
title: SQLServerBlob Constructor (SQLServerConnection, byte) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 76b8fe0d719a2eb5f53fe20502d0cd3fe35ca6eb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>SQLServerBlob Constructor (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) clase cuando se especifica un [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto y un **bytes** matriz.  
  
> [!NOTE]  
>  Este método se ha dejado de utilizar en la versión 2.0 del controlador JDBC. En su lugar, use la [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) método de la [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) clase.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *conexión*  
  
 Un objeto SQLServerConnection.  
  
 *datos*  
  
 A **bytes** matriz.  
  
## <a name="see-also"></a>Vea también  
 [Constructores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Miembros de SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  

