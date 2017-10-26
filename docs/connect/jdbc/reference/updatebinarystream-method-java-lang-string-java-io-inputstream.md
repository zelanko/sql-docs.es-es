---
title: "updateBinaryStream (método) (java.io.InputStream) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1fa688afc52a05664525a165930dca7ed7ac4b49
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="updatebinarystream-method-javalangstring-javaioinputstream"></a>Método updateBinaryStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo binario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateBinaryStream(java.lang.String columnLabel,  
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
 Este método updateBinaryStream especificado por el método updateBinaryStream en la interfaz java.sql.ResultSet.  
  
 Utiliza este método para el **imagen**, **texto**, y **ntext** tipos de datos de SQL Server podrían afectar al rendimiento.  
  
 Este método pasa bytes desde un objeto InputStream que seleccione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] columnas binarias como binary, varbinary, varbinary (max), image, xml y udt. Este método no admite la actualización de columnas de caracteres. Para actualizar las columnas de caracteres con un InputStream, use la [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md) método.  
  
## <a name="see-also"></a>Vea también  
 [Método updateBinaryStream &#40; SQLServerResultSet &#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Miembros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  

