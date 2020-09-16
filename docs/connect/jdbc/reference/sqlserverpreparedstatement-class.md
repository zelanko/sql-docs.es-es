---
description: Clase SQLServerPreparedStatement
title: Clase SQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 75a04a0873308cc09c16b54f5d482ed54a20c0b1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472147"
---
# <a name="sqlserverpreparedstatement-class"></a>Clase SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa la implementación básica de la funcionalidad de la instrucción preparada de JDBC.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** SQLServerStatement  
  
 **Implementa:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Observaciones  
 SQLServerPreparedStatement proporciona métodos que permiten especificar parámetros como cualquier tipo Java nativo y muchos tipos de objetos de Java. SQLServerPreparedStatement prepara una instrucción con el procedimiento almacenado  **sp_prepare** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, después, vuelve a usar el identificador de instrucciones devuelto cada vez que se ejecute la instrucción ulteriormente y, por lo general, se sirve de parámetros diferentes que proporciona el usuario.  
  
 SQLServerPreparedStatement admite el procesamiento por lotes, donde un conjunto de instrucciones preparadas se ejecuta en un ciclo de ida y vuelta en una misma base de datos, para mejorar el rendimiento en tiempo de ejecución.  
  
 Esta clase admite la desencapsulación en la clase SQLServerPreparedStatement, la interfaz ISQLServerPreparedStatement, la interfaz java.sql.PreparedStatement y las clases e interfaces que SQLServerStatement admite para desencapsular. Para más información, consulte [Contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
