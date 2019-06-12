---
title: Clase SQLServerStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ec24963c-8b51-4838-91e9-1fbfa2347451
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0901763b2f7b6c62e365df953012c2f54dba6f6d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776725"
---
# <a name="sqlserverstatement-class"></a>Clase SQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa la implementación básica de la funcionalidad de la instrucción de JDBC.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerStatement  
```  
  
## <a name="remarks"></a>Notas  
 La clase SQLServerStatement también proporciona varios métodos de implementación de la clase base para la instrucción preparada e instrucciones invocables de JDBC. El rol básico de la clase SQLServerStatement es ejecutar las instrucciones SQL y, a continuación, devolver los conteos de actualizaciones y conjuntos de resultados a la aplicación del usuario.  
  
 Esta clase admite la acción de desencapsular para la clase SQLServerStatement, la interfaz ISQLServerStatement y la interfaz java.sql.Statement. Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
