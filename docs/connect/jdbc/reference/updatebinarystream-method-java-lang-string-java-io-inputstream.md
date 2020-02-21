---
title: Método updateBinaryStream (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 56883144-26a0-4f45-ad36-4f616369af3e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc247cd3f97aeebeb6f52e1b4f3f36d8d97f6548
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67997161"
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
  
 Valor **string** que contiene la etiqueta de columna.  
  
 *x*  
  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Este método updateBinaryStream se especifica mediante el método updateBinaryStream de la interfaz java.sql.ResultSet.  
  
 El uso de este método con los tipos de datos de SQL Server **image**, **text** y **ntext** podría afectar al rendimiento.  
  
 Este método pasa bytes desde un objeto InputStream a las columnas binarias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seleccionadas, como binary, varbinary, varbinary(max), image, xml y udt. Este método no admite la actualización de columnas de caracteres. Para actualizar las columnas de caracteres con un elemento InputStream, use el método [updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método updateBinaryStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
