---
title: Método getNCharacterStream (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 45d2695b-0727-419d-8921-a51d6feef0aa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f46093aa08e6fcdbc769d76b11ca998744eed2e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66784622"
---
# <a name="getncharacterstream-method-javalangstring"></a>Método getNCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto Reader según el nombre del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.io.Reader getNCharacterStream(java.lang.String columnLabel)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnLabel*  
  
 Valor **string** que contiene la etiqueta de columna.  
  
## <a name="return-value"></a>Valor devuelto  
 AReaderobject.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método se debe usar al obtener acceso a **NCHAR**, **NVARCHAR** y **LONGNVARCHAR** parámetros.  
  
 Este método getNCharacterStream especificado por el método getNCharacterStream en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método getNCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getncharacterstream-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
