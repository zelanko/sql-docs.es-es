---
title: Método getCharacterStream (int) | Documentos de Microsoft
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
- SQLServerResultSet.getCharacterStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f9f230d-be4c-469a-b3dc-f24531429aae
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7541baecfd25c9c5cc65923686ab9bfb2dc6c51
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32832040"
---
# <a name="getcharacterstream-method-int"></a>Método getCharacterStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del índice de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto java.io.Reader.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.Reader getCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Un **int** que indica el índice de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getCharacterStream especificado por el método getCharacterStream en la interfaz java.sql.ResultSet.  
  
 Este método leerá solo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de datos de caracteres Unicode como nchar, nvarchar, nvarchar (max) y ntext. El resto de tipos de datos, incluso los tipos de carácter ASCII, producirán una excepción. Para leer los tipos de datos ASCII, utilice la [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Vea también  
 [Método getCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
