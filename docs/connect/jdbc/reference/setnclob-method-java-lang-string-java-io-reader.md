---
title: Método setNClob (java.lang.String, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a595679a-89b7-4b18-9ad2-d9cb13af2a28
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 252d16871a3aa161eacab99a62eaf4f8a2f03ae8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67973737"
---
# <a name="setnclob-method-javalangstring-javaioreader"></a>Método setNClob (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.io.Reader reader)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *reader*  
  
 Un objeto Reader.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Este método se debe usar para los tipos de datos de parámetros **NCHAR**, **NVARCHAR**, **NTEXT** y **XML**.  
  
 El método setNClob especifica este método setNClob en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método setNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
