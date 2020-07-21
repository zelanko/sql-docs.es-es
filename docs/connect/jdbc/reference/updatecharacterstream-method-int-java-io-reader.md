---
title: Método updateCharacterStream (int, java.io.Reader) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 4dddf885-0482-4776-8e9a-69f6c6270931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2639e3c886f04e6284b04055492674ade6ba90a8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928129"
---
# <a name="updatecharacterstream-method-int-javaioreader"></a>Método updateCharacterStream (int, java.io.Reader)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de flujo de caracteres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateCharacterStream(int columnIndex,  
                                  java.io.Reader x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
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
  
  
