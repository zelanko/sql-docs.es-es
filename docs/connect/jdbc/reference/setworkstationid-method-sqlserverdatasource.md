---
title: Método setWorkstationID (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setWorkstationID
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: c1093615-90bf-4918-9f05-8abd765ffb03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2c7664cb50f25d429ee74a163c589436bacf8902
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80901601"
---
# <a name="setworkstationid-method-sqlserverdatasource"></a>Método setWorkstationID (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre del equipo cliente que se utiliza para la conexión al origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setWorkstationID(java.lang.String workstationID)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *workstationID*  
  
 Un objeto **String** que contiene el nombre del equipo cliente.  
  
## <a name="remarks"></a>Observaciones  
 WorkstationID es el nombre del equipo cliente o de la estación de trabajo. Si no se establece la propiedad workstationID, el valor predeterminado se genera mediante una llamada al método InetAddress.getLocalHost().getHostName(). Si getHostName devuelve un valor en blanco, se llama al método getHostAddress().toString().  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
