---
title: "Método getScale (SQLServerParameterMetaData) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be05360747e2b67de20d6e93823b77629b5bbbac
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getscale-method-sqlserverparametermetadata"></a>Método getScale (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número de dígitos que se encuentran a la derecha del separador decimal para el parámetro designado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getScale(int param)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *param*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 En **int** que indica la escala del parámetro designado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getScale especificado por el método getScale en la interfaz java.sql.ParameterMetaData.  
  
 Este método obtiene los dígitos de la columna a la derecha del separador decimal. Para los tipos que no tienen un separador decimal, este método devuelve "0."  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Miembros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Clase SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  

