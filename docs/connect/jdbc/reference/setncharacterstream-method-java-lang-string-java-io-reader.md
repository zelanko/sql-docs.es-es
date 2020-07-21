---
title: 'Método setNCharacterStream para el objeto Reader: string | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fd19fbb8-a878-4d98-a584-e4969d649844
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 198bdc0fa291dd0c1786919ecaf2b6bb55aa36b1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80901241"
---
# <a name="setncharacterstream-method-javalangstring-javaioreader"></a>Método setNCharacterStream (java.lang.String, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el objeto Reader especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setNCharacterStream(java.lang.String parameterName,  
                       java.io.Reader value)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 Un valor **String** que indica el nombre del parámetro.  
  
 *value*  
  
 Un objeto Reader.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setNCharacterStream especifica este método setNCharacterStream en la interfaz java.sql.CallableStatement.  
  
 Este método se debe usar para los tipos de datos **NCHAR**, **NVARCHAR**, **NTEXT** y **XML**.  
  
## <a name="see-also"></a>Consulte también  
 [Método setNCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/setncharacterstream-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
