---
title: Método supportsSubqueriesInExists (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsSubqueriesInExists
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 14c08c7f-5c1e-4e21-8373-ae32c22e47d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22da8ae3f7f86501bdd15669c439a8d177ebd5f9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67968740"
---
# <a name="supportssubqueriesinexists-method-sqlserverdatabasemetadata"></a>Método supportsSubqueriesInExists (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite subconsultas en expresiones EXISTS.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsSubqueriesInExists()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsSubqueriesInExists especifica este método supportsSubqueriesInExists en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
