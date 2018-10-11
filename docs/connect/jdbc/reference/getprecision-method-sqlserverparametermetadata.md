---
title: Método getPrecision (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getPrecision
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8bd79484-bab6-423b-978f-d7ec7132ebeb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32913e5120afb71f4773318acc1b34c9daed892a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813303"
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
  
 Un valor **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica la precisión del parámetro designado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getPrecision especificado por el método getPrecision en la interfaz java.sql.ParameterMetaData.  
  
 Para los tipos de número, este método obtiene el número de dígitos decimales. Para los tipos de caracteres, obtiene la longitud máxima en caracteres. Para los tipos binarios, obtiene la longitud máxima en bytes. Cuando se desconozca el número de dígitos, este método devuelve "0."  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Miembros SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Clase SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
