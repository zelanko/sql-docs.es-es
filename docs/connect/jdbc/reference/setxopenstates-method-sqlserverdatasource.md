---
title: Método setXopenStates (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setXopenStates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9723591f-e987-426f-b70a-07f5c70dc094
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 43876cf7cdb829a8fc35862b6e9ec628f6f8b03f
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66773126"
---
# <a name="setxopenstates-method-sqlserverdatasource"></a>Método setXopenStates (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un valor **Boolean** que indica si está habilitada la conversión de estados SQL a estados conformes a XOPEN.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setXopenStates(boolean xopenStates)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *xopenStates*  
  
 **True** si está habilitada la conversión de Estados SQL a con XOpen. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad xopenStates se establece en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] convertirá los estados SQL en estados conformes a XOPEN. El valor predeterminado es **false**, que hace que el controlador JDBC genere códigos de estado de SQL 99. Si no se establece xopenStates, el método [getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md) devuelve el valor predeterminado **false**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
