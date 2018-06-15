---
title: Método getParameterClassName (SQLServerParameterMetaData) | Documentos de Microsoft
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
- SQLServerParameterMetaData.getParameterClassName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 545634d8-f06b-429a-9293-0087d758f359
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96ad9ab21829c19ee3e4b915287ad4e5d19a271b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836430"
---
# <a name="getparameterclassname-method-sqlserverparametermetadata"></a>Método getParameterClassName (SQLServerParameterMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el nombre completo de la clase Java cuyas instancias se deben pasar a la [setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) método de la [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getParameterClassName(int param)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *param*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre de clase completo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getParameterClassName especificado por el método getParameterClassName en la interfaz java.sql.ParameterMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-methods.md)   
 [Miembros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Clase SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-class.md)  
  
  
