---
title: "Método setIntegratedSecurity (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.setIntegratedSecurity
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5c82fad6b2fe56afe748b22ea8c131e8aff0e25d
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>Método setIntegratedSecurity (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un **booleano** valor que indica si la propiedad integratedSecurity está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *habilitar*  
  
 **True** si integratedSecurity está habilitada. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Comentarios  
 Establecido en "**true**" para indicar que va a usar credenciales de Windows por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] para autenticar al usuario de la aplicación. Si "**true**", la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] buscará en la caché de credenciales de equipo local para las credenciales que ya se ha proporcionado en el inicio de sesión de red o de equipo. Si "**false**", el nombre de usuario y la contraseña deben proporcionarse.  
  
> [!NOTE]  
>  Esta propiedad solo se admite en [!INCLUDE[msCoName](../../../includes/msconame_md.md)] sistemas operativos Windows.  
  
 Para obtener más información sobre el uso de la autenticación integrada, vea [generar URL de conexión](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
