---
title: "Método updateNCharacterStream (int, java.io.Reader) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc746413-bdbf-4109-aee0-385a1270c847
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0673e31672bbb9b3268f4b862406172c3eac0da7
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="updatencharacterstream-method-int-javaioreader"></a>Método updateNCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo de caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Un **int** que indica el índice de columna.  
  
 *x*  
  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateNCharacterStream especificado por el método updateNCharacterStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa los caracteres Unicode de un objeto de lector que seleccione **nchar**, **nvarchar (max)**, **ntext** y **xml** columnas. Si se utiliza este método en otras columnas de tipo de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Método updateNCharacterStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
