---
title: Método updateCharacterStream (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8ec22a9-4bbd-4759-9f21-957304ef3a5e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5300c381b7b64e90cdd9d6a9d3555ffce6a9af52
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67996667"
---
# <a name="updatecharacterstream-method-javalangstring-javaioreader"></a>Método updateCharacterStream (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo de caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateCharacterStream(java.lang.String columnLabel,  
                                  java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 Valor **string** que contiene la etiqueta de columna.  
  
 *reader*  
  
 Un objeto Reader.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Este método updateCharacterStream se especifica mediante el método updateCharacterStream de la interfaz java.sql.ResultSet.  
  
 Este método pasa los caracteres Unicode de un objeto Reader al texto seleccionado y las columnas binarias. Esto incluye todas las columnas de texto y las columnas **binary**, **varbinary**, **varbinary(max)** , **image** y **xml**, pero no las **udt**.  
  
 El uso de este método para los tipos de datos **image**, **text** y **ntext**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] podría afectar al rendimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
