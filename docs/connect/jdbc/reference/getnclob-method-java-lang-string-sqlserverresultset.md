---
description: Método getNClob (java.lang.String) (SQLServerResultSet)
title: Método getNClob (java.lang.String) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 36571f7c-b335-4249-8f83-51dcb6923aec
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9694239056ac410610874e31af35fea34ac8aa34
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435277"
---
# <a name="getnclob-method-javalangstring-sqlserverresultset"></a>Método getNClob (java.lang.String) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual del objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un objeto NClob en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.NClob getNClob(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 Valor **string** que contiene la etiqueta de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto NClob.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getNClob especifica este método getNClob en la interfaz java.sql.ResultSet.  
  
 Este método solo se admite en columnas **nvarchar (max)**, **ntext** y **xml**. Si se utiliza este método en cualquier otro tipo de datos, provocará una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getNClob &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
