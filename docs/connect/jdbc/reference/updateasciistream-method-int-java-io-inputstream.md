---
title: Método updateAsciiStream (java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1dcc3d4f-ae30-45c0-afad-a531358807af
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9acd8b75a7152a8e10faeb7f80d6d02c070ad2f0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67985521"
---
# <a name="updateasciistream-method-int-javaioinputstream"></a>Método updateAsciiStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo ASCII.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateAsciiStream(int columnIndex,  
                              java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método updateAsciiStream especifica este método updateAsciiStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa caracteres ASCII (bytes) desde un objeto InputStream a las columnas de caracteres convertibles, que son el rango ASCII [0x00 - 0x7F] de Unicode y las páginas de códigos 874, 932, 936, 949, 950 y desde la 1250 a la 1258. Este método realiza una conversión en la página de intercalación de destino. Si se intenta actualizar una columna de destino no convertible se producirá una excepción. Para las columnas binarias, se pasan bytes sin formato.  
  
 El uso de este método para los tipos de datos **image**, **text** y **ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podría afectar al rendimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateAsciiStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
