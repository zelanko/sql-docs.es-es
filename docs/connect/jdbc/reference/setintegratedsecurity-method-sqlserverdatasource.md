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
ms.openlocfilehash: 79d9090df19851af3a778e23b7919f28081f32ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974145"
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
  
 **true** si integratedSecurity está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Se establece en "**true**" para indicar que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] va a usar credenciales de Windows para autenticar al usuario de la aplicación. Si el valor es "**true**", el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] buscará en la memoria caché de credenciales del equipo local suministradas en el equipo o en el inicio de sesión de red. Si el valor es "**false**", se debe suministrar el nombre de usuario y la contraseña.  
  
> [!NOTE]  
>  Esta propiedad solo se admite en los sistemas operativos de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] Windows.  
  
 Para obtener más información sobre el uso de la autenticación integrada, vea [crear la dirección URL de conexión](../../../connect/jdbc/building-the-connection-url.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
