---
title: "Método setIntegratedSecurity (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b0480212d2216f66d917debcd7565093d89c9d78
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

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
  
  

