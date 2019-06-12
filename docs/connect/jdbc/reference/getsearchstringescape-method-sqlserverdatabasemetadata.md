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
manager: jroth
ms.openlocfilehash: 715787197357f6d10f0d116359155c86edb07187
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792051"
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
 Este método getSearchStringEscape especificado por el método getSearchStringEscape en la interfaz java.sql.DatabaseMetaData.  
  
 Este método solamente se utiliza para las búsquedas de modelos de metadatos. Devuelve "\\". Un modelo de búsqueda **String** puede establecer como caracteres de escape a los caracteres comodín ("%" y "_") y suministrarlos como literales anteponiendo una barra diagonal inversa. Esto convierte "\\%" en "[%]" y "\\\_" en "[\_]".  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
