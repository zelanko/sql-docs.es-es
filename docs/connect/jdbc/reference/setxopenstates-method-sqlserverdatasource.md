---
title: Método setXopenStates (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 201c0b34da3198ed0f6067944d581fb9bc696bd4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>Método setXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un **booleano** valor que indica si está habilitada la conversión de Estados SQL Estados conformes a XOPEN.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *xopenStates*  
  
 **True** si está habilitada la conversión de Estados SQL Estados conformes a XOPEN. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Comentarios  
 Si la propiedad xopenStates se establece en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] convertirá Estados SQL a Estados conformes a XOPEN. El valor predeterminado es **false**, lo que hace que el controlador JDBC generar códigos de estado SQL 99. Si no se establece xopenStates, el [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) método devuelve el valor predeterminado de **false**.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
