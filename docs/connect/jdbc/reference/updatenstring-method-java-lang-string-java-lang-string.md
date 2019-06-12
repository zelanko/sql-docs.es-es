---
title: Método updateNString (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6daca03f-c60f-4842-b9e3-11d136e78312
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a6451896913876c3694a72e877c449109c61ac0b
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776674"
---
# <a name="updatenstring-method-javalangstring-javalangstring"></a>Método updateNString (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor **string** mediante el uso de la etiqueta de columna especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateNString(java.lang.String columnLabel,  
                          java.lang.String nString)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 Valor **string** que contiene la etiqueta de columna.  
  
 *nString*  
  
 Un **cadena** objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método updateNString especificado por el método updateNString en la interfaz java.sql.ResultSet.  
  
 Este método pasa Java **cadena** a activado **nchar**, **nvarchar (max)** , **ntext**, y **xml** columnas. Si se utiliza este método en otras columnas de tipo de datos, se producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [updateNString (método) &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
