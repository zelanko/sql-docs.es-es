---
title: Método getDateTimeOffset (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8bb00356-4d6e-4625-b924-67646930fdf2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: a83bb0d142860b1cb6f94070b8a85f3c40b23114
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777035"
---
# <a name="getdatetimeoffset-method-int"></a>Método getDateTimeOffset (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Recupera el valor del parámetro designado como un objeto [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) en el lenguaje de programación Java según el índice de parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 El ordinal del parámetro que se basa en uno.  
  
## <a name="return-value"></a>Valor devuelto  
 Un [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Puede establecer un [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor de parámetro con [SQLServerCallableStatement.setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método getDateTimeOffset &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
