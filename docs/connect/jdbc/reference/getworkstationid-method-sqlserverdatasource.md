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
ms.openlocfilehash: 98cde4953d60f13d1768b06dbfab9ada6ea8af55
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978049"
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
  
## <a name="remarks"></a>Observaciones  
 WorkstationID es el nombre del equipo cliente o de la estación de trabajo. Si no se establece la propiedad workstationID, el valor predeterminado se genera mediante una llamada al método InetAddress.getLocalHost().getHostName(). Si getHostName devuelve un valor en blanco, se llama al método getHostAddress().toString().  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
