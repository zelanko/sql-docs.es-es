---
title: Método supportsCatalogsInPrivilegeDefinitions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCatalogsInPrivilegeDefinitions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cc18f99e-c19f-4bd0-96ae-b9a6a0de1926
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 16a57ee05bbe67d4fe8a88f61d969f79734521cd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67969692"
---
# <a name="supportscatalogsinprivilegedefinitions-method-sqlserverdatabasemetadata"></a>Método supportsCatalogsInPrivilegeDefinitions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si un nombre de catálogo se puede utilizar en una instrucción de definición de privilegios.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsCatalogsInPrivilegeDefinitions()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsCatalogsInPrivilegeDefinitions especifica este método supportsCatalogsInPrivilegeDefinitions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
