---
title: Método setNClob (int, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 48c8aa2a-4185-4837-b592-830e60f8ca0b
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 3120c101a8c57225bc709da3066080987943d3c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800420"
---
# <a name="setnclob-method-int-javasqlnclob"></a>Método setNClob (int, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto NClob especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNClob(int parameterIndex,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterIndex*  
  
 Un valor **int** que indica el índice del parámetro.  
  
 *value*  
  
 Un objeto NClob que indica el valor del parámetro.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El método setNClob especifica este método setNClob en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método setNClob &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)   
 [Miembros SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
