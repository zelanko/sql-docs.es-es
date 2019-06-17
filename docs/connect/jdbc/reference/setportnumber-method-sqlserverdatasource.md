---
title: Método setPortNumber (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 59c5fa23-bc1a-4142-af17-70e275f0b833
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 304d63f7822990c4d8e4a9c0787c9e688c222580
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799629"
---
# <a name="setportnumber-method-sqlserverdatasource"></a>Método setPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de puerto que se va a utilizar para la comunicación con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setPortNumber(int portNumber)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *portNumber*  
  
 Valor **int** que contiene el número de puerto.  
  
## <a name="remarks"></a>Notas  
 El número de puerto es el número del puerto TCP/IP que se utiliza al abrir una conexión de socket con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se establece la propiedad portNumber, el método [getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md) devuelve el valor predeterminado de 1433.  
  
> [!NOTE]  
>  El método setPortNumber no hace ninguna comprobación en el pasado en el valor del puerto del intervalo. Puede pasar un número de puerto que no es válido, como 99999, sin desencadenar un error.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
