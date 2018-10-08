---
title: Método supportsOpenCursorsAcrossRollback | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsOpenCursorsAcrossRollback
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4bc3e82b-a7e7-43a5-8938-6f29c7570163
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3a1dc525ba0d2be1a4bba4cdbee70365dfecc1bc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840823"
---
# <a name="supportsopencursorsacrossrollback-method-sqlserverdatabasemetadata"></a>Método supportsOpenCursorsAcrossRollback (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos permite mantener cursores abiertos en las reversiones.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsOpenCursorsAcrossRollback()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método supportsOpenCursorsAcrossRollback especificado por el método supportsOpenCursorsAcrossRollback en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
