---
title: Método setNClob (java.lang.String, java.sql.NClob) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4e30d242-0c1b-45db-b75f-41b041692f31
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bb011b7d2b0a3b18576765ebeaf3d9c75fa636e1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923283"
---
# <a name="setnclob-method-javalangstring-javasqlnclob"></a>Método setNClob (java.lang.String, java.sql.NClob)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto NClob especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNClob(java.lang.String parameterName,  
              java.sql.NClob value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *value*  
  
 Un objeto NClob.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Este método se debe usar para los tipos de datos de parámetros **NCHAR**, **NVARCHAR**, **NTEXT** y **XML**.  
  
 El método setNClob especifica este método setNClob en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método setNClob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setnclob-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
