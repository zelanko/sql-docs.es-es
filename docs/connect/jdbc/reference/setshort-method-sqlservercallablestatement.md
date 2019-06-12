---
title: Método setShort (SQLServerCallableStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.setShort
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d7031a89-e964-4ffd-87b7-63825799435d
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f2bdaf864cba4c95459a2db8f558404c42943d99
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66782898"
---
# <a name="setshort-method-sqlservercallablestatement"></a>Método setShort (SQLServerCallableStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el valor **short** determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setShort(java.lang.String sCol,  
                     short s)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *s*  
  
 Un **corto** valor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método setShort especifica este método setShort en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
