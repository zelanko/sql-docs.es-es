---
title: Método isNullable (SQLServerParameterMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.sNullable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d7e07cff-6fc4-4c9c-8e8f-838c77734bc5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3e49934129bc4da9bdc576eab3e252636dd5a60
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="isnullable-method-sqlserverparametermetadata"></a>Método isNullable (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si se permiten valores NULL en el parámetro designado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int isNullable(int param)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *param*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica la nulabilidad del parámetro designado, que puede ser uno de los siguientes valores:  
  
 ParameterMetaData.parameterNoNulls  
  
 ParameterMetaData.parameterNullable  
  
 ParameterMetaData.parameterNullabilityUnknown  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método isNullable es especificado por el método isNullable en la interfaz java.sql.ParameterMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Miembros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Clase SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
