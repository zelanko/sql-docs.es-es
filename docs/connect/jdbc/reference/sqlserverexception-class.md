---
title: Clase SQLServerException | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: afaffe76cecaf1b0e6a99eb49c46d8b77c72a746
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32846880"
---
# <a name="sqlserverexception-class"></a>Clase SQLServerException
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa una ejecución de una instrucción SQL que se ha realizado de forma incorrecta o incompleta.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.sql.SQLException  
  
 **Implementa:** java.io.Serializable  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final class SQLServerException  
```  
  
## <a name="remarks"></a>Comentarios  
 La clase SQLServerException controla los códigos de estado SQL 92 y XOPEN. Se pueden intercambiar si se utiliza una propiedad de conexión que determine el usuario. Las excepciones se escriben en cualquier archivo de registro abierto que se haya especificado.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
