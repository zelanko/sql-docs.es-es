---
title: Método setIntegratedSecurity (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setIntegratedSecurity
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c968ee4-b041-424a-bf69-cc2c4a4f51c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7d922c2c2fcfadb6b7807b8d2845f8d3e6c5188c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780452"
---
# <a name="setintegratedsecurity-method-sqlserverdatasource"></a>Método setIntegratedSecurity (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un valor **Boolean** que indica si la propiedad integratedSecurity está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setIntegratedSecurity(boolean enable)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *enable*  
  
 **True** si integratedSecurity está habilitada. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Se establece en "**true**" para indicar que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] va a usar credenciales de Windows para autenticar al usuario de la aplicación. Si el valor es "**true**", el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] buscará en la memoria caché de credenciales del equipo local suministradas en el equipo o en el inicio de sesión de red. Si el valor es "**false**", se debe suministrar el nombre de usuario y la contraseña.  
  
> [!NOTE]  
>  Esta propiedad solo se admite en los sistemas operativos de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows.  
  
 Para obtener más información sobre el uso de la autenticación integrada, vea [generar URL de conexión](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
