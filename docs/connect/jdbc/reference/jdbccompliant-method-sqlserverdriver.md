---
title: Método jdbcCompliant (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.jdbcCompliant
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b299b20d-d1cd-45b3-91dc-dcf579498570
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c36d7980355eed1e1a1e8f42fb53c75fdb70d0ed
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67976948"
---
# <a name="jdbccompliant-method-sqlserverdriver"></a>Método jdbcCompliant (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Comprueba que [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] es conforme a la especificación JDBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean jdbcCompliant()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el controlador JDBC cumple los requisitos mínimos. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 El método jdbcCompliant especifica este método jdbcCompliant en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
