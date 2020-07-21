---
title: Método getMaxSchemaNameLength (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getMaxSchemaNameLength
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fece19e9-3bf8-4299-9188-ac3df5ce9c19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 93a6447a2784d4b6a70392f7886cb1c5ed68c8f8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80906581"
---
# <a name="getmaxschemanamelength-method-sqlserverdatabasemetadata"></a>Método getMaxSchemaNameLength (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número máximo de caracteres que esta base de datos permite en un nombre de esquema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getMaxSchemaNameLength()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica el número máximo permitido de caracteres.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getMaxSchemaNameLength especifica este método getMaxSchemaNameLength en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
