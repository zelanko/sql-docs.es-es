---
title: "Método getPrecision (SQLServerParameterMetaData) | Documentos de Microsoft"
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
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8c80beecc510fb5f2d4190839e8bc4ca1c95602c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getprecision-method-sqlserverparametermetadata"></a>Método getPrecision (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el número de dígitos decimales del parámetro designado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getPrecision(int param)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *param*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** que indica la precisión del parámetro designado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getPrecision especificado por el método getPrecision en la interfaz java.sql.ParameterMetaData.  
  
 Para los tipos de número, este método obtiene el número de dígitos decimales. Para los tipos de caracteres, obtiene la longitud máxima en caracteres. Para los tipos binarios, obtiene la longitud máxima en bytes. Cuando se desconozca el número de dígitos, este método devuelve "0."  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Miembros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Clase SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
