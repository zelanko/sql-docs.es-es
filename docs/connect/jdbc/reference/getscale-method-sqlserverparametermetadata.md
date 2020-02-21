---
title: Método getScale (SQLServerParameterMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerParameterMetaData.getScale
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7b8d8d9c-74aa-4e6e-88f1-2fc5c74004ae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 29c2da8d8b6645ec9d5186f79db80b03626b2978
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67980203"
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
  
 Un valor **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int** que indica la escala del parámetro designado.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getScale especifica este método getScale en la interfaz java.sql.ParameterMetaData.  
  
 Este método obtiene los dígitos de la columna a la derecha del separador decimal. Para los tipos que no tienen un separador decimal, este método devuelve "0."  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Miembros SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Clase SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
