---
title: Método storesMixedCaseIdentifiers (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.storesMixedCaseIdentifiers
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a91e5cd6-22b1-464e-aeec-665590737a74
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a1d1a924b913ecffc4baea959053001d7e30c1db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67969900"
---
# <a name="storesmixedcaseidentifiers-method-sqlserverdatabasemetadata"></a>Método storesMixedCaseIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos trata a los identificadores de SQL con combinaciones de mayúsculas y minúsculas que no se entrecomillan como elementos que distinguen entre mayúsculas y minúsculas y los almacena combinando ambos formatos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean storesMixedCaseIdentifiers()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si los identificadores están almacenados combinando mayúsculas y minúsculas. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método storesMixedCaseIdentifiers especifica este método storesMixedCaseIdentifiers en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
