---
title: Método updateNString (int, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1bb909f1-4a96-4be1-adea-36c8d9703112
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90aa44eda2af60ffdc73a65e01b3ae12b949d79f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67998797"
---
# <a name="updatenstring-method-int-javalangstring"></a>Método updateNString (int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor **String** mediante el uso del índice de la columna especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNString(int columnIndex,  
                        java.lang.String nString)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
 *nString*  
  
 Un objeto **String**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateNString especifica este método updateNString en la interfaz java.sql.ResultSet.  
  
 Este método pasa **String** de Java a columnas **nchar**, **nvarchar(max)** , **ntext** y **xml** seleccionadas. Si se utiliza este método en otras columnas de tipo de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [updateNString (método) &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
