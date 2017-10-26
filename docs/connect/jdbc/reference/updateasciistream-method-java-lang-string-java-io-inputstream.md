---
title: "Método (java.io.InputStream) updateAsciiStream | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 747b0308-1ce6-4eba-bdfc-af29c21c18cf
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b7885895db612ffd4fd6801cea64242ad9347859
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updateasciistream-method-javalangstring-javaioinputstream"></a>Método updateAsciiStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo ASCII.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateAsciiStream(java.lang.String columnLabel,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 A **cadena** que contiene la etiqueta de columna.  
  
 *x*  
  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método updateAsciiStream especificado por el método updateAsciiStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa caracteres ASCII (bytes) de un objeto InputStream a las columnas de caracteres convertibles, que son el rango ASCII [0 x 00 a 0x7F] de Unicode y 874, 932, 936, 949, 950 y desde la 1250 a las páginas de códigos 1258. Este método realiza una conversión en la página de intercalación de destino. Si se intenta actualizar una columna de destino no convertible se producirá una excepción. Para las columnas binarias, se pasan bytes sin formato.  
  
 Utiliza este método para el **imagen**, **texto**, y **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipos de datos podrían afectar al rendimiento.  
  
## <a name="see-also"></a>Vea también  
 [Método updateAsciiStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

