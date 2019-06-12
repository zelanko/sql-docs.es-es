---
title: Método isReadOnly (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.isReadOnly
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d1569e03-b7bd-486a-af0b-d3f108f712dc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c9d557bf62961a02c24564a6f32516b4b98ef425
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796400"
---
# <a name="isreadonly-method-sqlserverdatabasemetadata"></a>Método isReadOnly (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos está en modo de solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isReadOnly()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si la base de datos está en modo de solo lectura. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método isReadOnly es especificado por el método isReadOnly en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
