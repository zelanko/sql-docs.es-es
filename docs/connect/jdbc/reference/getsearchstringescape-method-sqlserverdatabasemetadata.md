---
title: Método getSearchStringEscape (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getSearchStringEscape
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ea0f95d0-0238-4dc8-9f26-7ff9b65f30c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1b65281fbe6ba1f758bdd4e12ae834cee3347842
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980051"
---
# <a name="getsearchstringescape-method-sqlserverdatabasemetadata"></a>Método getSearchStringEscape (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el objeto **String** que se puede utilizar para establecer como carácter de escape a los caracteres comodín.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getSearchStringEscape()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String** que contiene la cadena de caracteres comodín de escape.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getSearchStringEscape se especifica mediante el método getSearchStringEscape en la interfaz java. SQL. DatabaseMetaData.  
  
 Este método solamente se utiliza para las búsquedas de modelos de metadatos. Devuelve "\\". Un modelo de búsqueda **String** puede establecer como caracteres de escape a los caracteres comodín ("%" y "_") y suministrarlos como literales anteponiendo una barra diagonal inversa. Esto convierte "\\%" en "[%]" y "\\\_" en "[\_]".  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
