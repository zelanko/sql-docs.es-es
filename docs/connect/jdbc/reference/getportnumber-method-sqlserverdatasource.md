---
title: Método getPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20850d10352a583abd7e0a8bd9747b6346ec3aaa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67980836"
---
# <a name="getportnumber-method-sqlserverdatasource"></a>Método getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el número de puerto actual que se utiliza para la comunicación con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **int** que contiene el número de puerto actual.  
  
## <a name="remarks"></a>Notas  
 El número de puerto es el número del puerto TCP/IP que se utiliza al abrir una conexión de socket con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece la propiedad portNumber, el método getPortNumber devuelve el valor predeterminado de 1433.  
  
> [!NOTE]  
>  El método [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) no realiza ninguna comprobación de intervalo en el valor de Puerto pasado. Puede pasar números de agravios que no sean válidos, como 99999, sin desencadenar un error.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
