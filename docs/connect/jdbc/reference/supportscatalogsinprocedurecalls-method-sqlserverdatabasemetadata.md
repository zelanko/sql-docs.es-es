---
title: Método supportsCatalogsInProcedureCalls | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInProcedureCalls
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5ec3571a-c7c6-4b94-a9ea-ac08adc7f978
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e9f6532ca8f23a9e8d729bccc204865860e71ac9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969685"
---
# <a name="supportscatalogsinprocedurecalls-method-sqlserverdatabasemetadata"></a>Método supportsCatalogsInProcedureCalls (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si un nombre de catálogo se puede utilizar en una instrucción de llamada a procedimientos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsCatalogsInProcedureCalls()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsCatalogsInProcedureCalls especifica este método supportsCatalogsInProcedureCalls en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
