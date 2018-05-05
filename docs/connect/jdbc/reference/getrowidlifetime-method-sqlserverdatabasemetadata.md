---
title: Método getRowIdLifetime (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 317c0b44-fe3f-4142-9cab-e40e4c4fe070
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b446ecaed7ff20ced714e93e6ce3f4756bcd0ce9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getrowidlifetime-method-sqlserverdatabasemetadata"></a>Método getRowIdLifetime (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un estado que indica si se admite el tipo de datos RowId de SQL. Si así fuera, devuelve la duración de un objeto RowId.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.RowIdLifetime getRowIdLifetime()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto RowIdLifetime.  
  
> [!NOTE]  
>  En la versión de la versión 2.0 del controlador JDBC, este método devuelve el valor de java.sql.RowIdLifetime.ROWID_UNSUPPORTED.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getRowIdLifetime especificado por el método getRowIdLifetime en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
