---
title: Método getCatalog (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.getCatalog
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e87ef65f-4b5a-4e1c-8db5-7f0932390bb0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0f6d74b8dee21333c1358a9f998371e38b5c0cd
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953343"
---
# <a name="getcatalog-method-sqlserverconnection"></a>Método getCatalog (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el nombre del catálogo actual para este objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getCatalog()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene el nombre del catálogo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getCatalog especifica este método getCatalog en la interfaz java.sql.Connection.  
  
 Devuelve la propiedad de catálogo actual del objeto SQLServerConnection, o bien NULL se no se ha establecido. La propiedad de catálogo se establece explícitamente con el método [setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md) o se actualiza implícitamente mediante la lectura del cambio del entorno en el TDS correspondiente al catálogo actual.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
