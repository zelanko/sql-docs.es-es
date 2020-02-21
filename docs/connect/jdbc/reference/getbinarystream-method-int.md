---
title: Método getBinaryStream (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBinaryStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: de22a6c4-1ba3-4ed0-91a2-bf235c2ceec3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e0add171861f2ea9e021b9f9342968baf1601557
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67953709"
---
# <a name="getbinarystream-method-int"></a>Método getBinaryStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del índice de la columna designada en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo binario de bytes sin interpretar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.io.InputStream getBinaryStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getBinaryStream especifica este método getBinaryStream en la interfaz java.sql.ResultSet.  
  
 Este método solamente se puede utilizar con tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] binary, varbinary, varbinary(max) e image. Si se intenta utilizar con cualquier otro tipo de datos, provocará una excepción.  
  
 Una vez que este método obtenga el valor como un flujo, el valor se puede leer en fragmentos desde el flujo. Este método es particularmente conveniente para recuperar valores LONGVARBINARY grandes.  
  
> [!NOTE]  
>  Todos los datos en el flujo devuelto se deben leer antes de obtener el valor de cualquier otra columna. La llamada siguiente a un método de captador cierra el flujo implícitamente. Además, un flujo puede devolver 0 cuando se llama al método InputStream.available, independientemente de que haya datos disponibles o no.  
  
## <a name="see-also"></a>Consulte también  
 [Método getBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
