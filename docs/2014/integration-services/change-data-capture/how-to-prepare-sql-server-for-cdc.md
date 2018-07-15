---
title: Cómo preparar SQL Server para CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 061fbc80b705b03e1bfa399d6362fbc1536ae15d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252637"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>Cómo preparar SQL Server para CDC
  El servicio CDC de Oracle necesita que todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contengan la base de datos MSXDBCDC. Esta base de datos se crea mediante la acción Preparar SQL Server de la Consola de configuración del servicio CDC. Esta tarea se realiza una sola vez para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 A continuación se describe cómo preparar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la captura de datos modificados de Oracle mediante la Consola de configuración del servicio CDC. Este proceso crea la base de datos MSXDBCDC y define las tablas, los procedimientos almacenados y otros artefactos necesarios.  
  
 La preparación de SQL Server para CDC de Oracle se realiza mediante el administrador del servicio CDC de Oracle. Para obtener más información sobre el rol de administrador del servicio CDC, vea [Roles de usuario para Change Data Capture Service para Oracle de Attunity](user-roles.md).  
  
### <a name="to-enable-sql-server-for-cdc"></a>Para habilitar SQL Server para CDC  
  
1.  En el menú **Inicio** , seleccione **Configuración del servicio CDC para Oracle**.  
  
2.  En el panel izquierdo, seleccione **Servicios CDC locales** y a continuación, en el panel **Acciones** , haga clic en **Preparar SQL Server**.  
  
     También puede hacer clic con el botón derecho en **Local CDC Services** (Servicios CDC locales) y seleccionar **Prepare SQL Server**(Preparar SQL Server).  
  
3.  Escriba la información necesaria en el cuadro de diálogo Preparando instancia de SQL Server para CDC de Oracle. Para obtener información acerca de cómo especificar la información necesaria en este cuadro de diálogo, vea [Prepare SQL Server for CDC](prepare-sql-server-for-cdc.md).  
  
     Para preparar la instancia de SQL Server para CDC de Oracle, el inicio de sesión debe tener permiso de escritura para la base de datos MSXDBCDC. Escriba las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como un miembro del rol `sysasmin` .  
  
 **Nota**: Puede hacer clic en **Ver script** para ver una versión de solo lectura del script de configuración. Un administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar este script en la consola de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para editarlo y ejecutarlo, si es necesario.  
  
## <a name="see-also"></a>Vea también  
 [Preparar SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
  
