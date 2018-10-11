---
title: Miembros SQLServerNClob | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b063f191-175e-4430-aab7-d88907f4ebec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81bcb5406a491d0e7b73ec098b160008c1a11c4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47795543"
---
# <a name="sqlservernclob-members"></a>Miembros SQLServerNClob
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  En las siguientes tablas se enumeran los miembros que expone la clase [SQLServerNClob](../../../connect/jdbc/reference/sqlservernclob-class.md).  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
 Ninguno.  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[free](../../../connect/jdbc/reference/free-method-sqlservernclob.md)|Este método libera el objeto **NCLOB** y los recursos que contiene.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlservernclob.md)|Recupera el **NCLOB** valor designado por el **java.sql.NClob** objeto como un flujo ASCII.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlservernclob.md)|Recupera el **NCLOB** valor designado por el **java.sql.NClob** objeto.|  
|[getSubString](../../../connect/jdbc/reference/getsubstring-method-sqlservernclob.md)|Recupera una copia de la subcadena especificada en el **NCLOB** valor designado por el **java.sql.NClob** objeto.|  
|[length](../../../connect/jdbc/reference/length-method-sqlservernclob.md)|Recupera el número de caracteres en el **NCLOB** valor designado por el **java.sql.NClob** objeto.|  
|[position](../../../connect/jdbc/reference/position-method-sqlservernclob.md)|Recupera la posición del carácter especificado **java.sql.NClob** de objeto o subcadena en el **java.sql.NClob** basándose en la posición inicial especificada.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlservernclob.md)|Recupera un flujo que se va a utilizar para escribir caracteres ASCII para el valor **NCLOB** que representa este objeto **java.sql.NClob**, a partir de la posición especificada.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlservernclob.md)|Recupera un flujo que se va a utilizar para escribir un flujo de Unicode para el valor **NCLOB** que representa este objeto **Java.sql.NClob**, a partir de la posición especificada.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlservernclob.md)|Escribe el determinado **cadena** a la **NCLOB** empezando en la posición especificada.|  
|[truncate](../../../connect/jdbc/reference/truncate-method-sqlservernclob.md)|Trunca el **NCLOB** valor a la longitud especificada.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de|Métodos|  
|--------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Clob|free, getAsciiStream, getCharacterStream, getSubString, length, position, setAsciiStream, setCharacterStream, setString, truncate|  
  
## <a name="see-also"></a>Ver también  
 [Clase SQLServerClob](../../../connect/jdbc/reference/sqlserverclob-class.md)  
  
  
