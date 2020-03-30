---
title: Método getMaxCatalogNameLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxCatalogNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 89c11327-eae1-4178-9e26-4b484d521c65
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ff0e29e95b321d912f19cece28fd1579aeff50a2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67982356"
---
# <a name="getmaxcatalognamelength-method-sqlserverdatabasemetadata"></a>Método getMaxCatalogNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de caracteres que esta base de datos permite en un nombre de catálogo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMaxCatalogNameLength()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número máximo permitido de caracteres.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getMaxCatalogNameLength especifica este método getMaxCatalogNameLength en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
