---
title: Método getExtraNameCharacters (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getExtraNameCharacters
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: a22becfe-0f07-4a15-8d11-06d4054b2369
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a4aada79019aad4ae01729de8e018edd728b473
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67983314"
---
# <a name="getextranamecharacters-method-sqlserverdatabasemetadata"></a>Método getExtraNameCharacters (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera todos los caracteres adicionales que se pueden utilizar en nombres de identificador sin comillas, por ejemplo, aquellos que no sean a-z, A-Z, 0-9 y _.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getExtraNameCharacters()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **string** que contiene los caracteres adicionales.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getExtraNameCharacters especifica este método getExtraNameCharacters en la interfaz java.sql.DatabaseMetaData.  
  
 Cuando se usa [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método devuelve los caracteres adicionales $, # y \@.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
