---
title: Método updateCharacterStream (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8ec22a9-4bbd-4759-9f21-957304ef3a5e
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88ce3b6db5911aa881907c1b4d80dd59d0f416b2
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2018
ms.locfileid: "42787274"
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
  
 Un objeto lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método updateCharacterStream especificado por el método updateCharacterStream en la interfaz java.sql.ResultSet.  
  
 Este método pasa los caracteres Unicode de un objeto Reader al texto seleccionado y las columnas binarias. Esto incluye todas las columnas de texto y las columnas **binary**, **varbinary**, **varbinary(max)**, **image** y **xml**, pero no las **udt**.  
  
 Con este método para el **imagen**, **texto**, y **ntext** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos podrían afectar al rendimiento.  
  
## <a name="see-also"></a>Ver también  
 [Método updateCharacterStream &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
