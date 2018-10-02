---
title: Cómo preparar SQL Server para CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 731912d437b0a0a5c277fe2f9496fa2b6b5be440
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47770199"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>Cómo preparar SQL Server para CDC
  El servicio CDC de Oracle necesita que todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contengan la base de datos MSXDBCDC. Esta base de datos se crea mediante la acción Preparar SQL Server de la Consola de configuración del servicio CDC. Esta tarea se realiza una sola vez para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 A continuación se describe cómo preparar una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la captura de datos modificados de Oracle mediante la Consola de configuración del servicio CDC. Este proceso crea la base de datos MSXDBCDC y define las tablas, los procedimientos almacenados y otros artefactos necesarios.  
  
 La preparación de SQL Server para CDC de Oracle se realiza mediante el administrador del servicio CDC de Oracle. Para obtener más información acerca del rol de administrador del servicio CDC, vea [User Roles](../../integration-services/change-data-capture/user-roles.md).  
  
### <a name="to-enable-sql-server-for-cdc"></a>Para habilitar SQL Server para CDC  
  
1.  En el menú **Inicio** , seleccione **Configuración del servicio CDC para Oracle**.  
  
2.  En el panel izquierdo, seleccione **Servicios CDC locales** y a continuación, en el panel **Acciones** , haga clic en **Preparar SQL Server**.  
  
     También puede hacer clic con el botón derecho en **Local CDC Services** (Servicios CDC locales) y seleccionar **Prepare SQL Server**(Preparar SQL Server).  
  
3.  Escriba la información necesaria en el cuadro de diálogo Preparando instancia de SQL Server para CDC de Oracle. Para obtener información acerca de cómo especificar la información necesaria en este cuadro de diálogo, vea [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md).  
  
     Para preparar la instancia de SQL Server para CDC de Oracle, el inicio de sesión debe tener permiso de escritura para la base de datos MSXDBCDC. Escriba las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como un miembro del rol `sysasmin` .  
  
 **Nota**: Puede hacer clic en **Ver script** para ver una versión de solo lectura del script de configuración. Un administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar este script en la consola de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para editarlo y ejecutarlo, si es necesario.  
  
## <a name="see-also"></a>Ver también  
 [Preparar SQL Server para CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
