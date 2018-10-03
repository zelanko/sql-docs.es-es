---
title: Método getBinaryStream (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 149609b5-a6de-4e23-a440-7061775d0899
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85f46fb35979bcf7111e2596b4d12c48160ebcdc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47644043"
---
# <a name="getbinarystream-method-javalangstring"></a>Método getBinaryStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del nombre de la columna designada en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo binario de bytes sin interpretar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.InputStream getBinaryStream(java.lang.String columnName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnName*  
  
 Valor **String** que contiene el nombre de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getBinaryStream especificado por el método getBinaryStream en la interfaz java.sql.ResultSet.  
  
 Este método solamente se puede utilizar con tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] binary, varbinary, varbinary(max) e image. Si se intenta utilizar con cualquier otro tipo de datos, provocará una excepción.  
  
 Una vez que este método obtenga el valor como un flujo, el valor se puede leer en fragmentos desde el flujo. Este método es particularmente conveniente para recuperar valores LONGVARBINARY grandes.  
  
> [!NOTE]  
>  Todos los datos en el flujo devuelto se deben leer antes de obtener el valor de cualquier otra columna. La llamada siguiente a un método de captador cierra el flujo implícitamente. Además, un flujo puede devolver 0 cuando se llama al método InputStream.available, independientemente de que haya datos disponibles o no.  
  
## <a name="see-also"></a>Ver también  
 [Método getBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
