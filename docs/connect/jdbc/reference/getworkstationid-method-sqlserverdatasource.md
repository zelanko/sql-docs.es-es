---
title: Método getWorkstationID (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f6a701de-a8fa-4668-9310-99a8c6e32c88
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 117c0ad7ff08cec0c3c0b39758dce1dc55ecb249
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66779886"
---
# <a name="getworkstationid-method-sqlserverdatasource"></a>Método getWorkstationID (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre del nombre del equipo cliente que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getWorkstationID()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto **String** que contiene el nombre del equipo cliente.  
  
## <a name="remarks"></a>Notas  
 WorkstationID es el nombre del equipo cliente o de la estación de trabajo. Si no se establece la propiedad workstationID, el valor predeterminado se construye llamando al método InetAddress.getLocalHost().getHostName(). Si getHostName devuelve un valor en blanco, se llama al método getHostAddress().toString().  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
