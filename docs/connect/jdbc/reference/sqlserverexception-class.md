---
description: Clase SQLServerException
title: Clase SQLServerException | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: af5ef257-7cf6-4db3-b1ee-07d22d82bef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b096f1b41cc817b216cea9ff3618e7731abd5003
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450541"
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
  
## <a name="remarks"></a>Observaciones  
 La clase SQLServerException controla los códigos de estado SQL 92 y XOPEN. Se pueden intercambiar si se utiliza una propiedad de conexión que determine el usuario. Las excepciones se escriben en cualquier archivo de registro abierto que se haya especificado.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerException](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
