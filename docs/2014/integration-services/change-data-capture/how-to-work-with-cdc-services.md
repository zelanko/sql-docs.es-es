---
title: Cómo trabajar con CDC Service | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: db5c718a-6e7f-48ec-82a3-9d5b131716e5
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5479449337e507802727472cebe85dc4452d7dfe
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200594"
---
# <a name="how-to-work-with-cdc-services"></a>Cómo trabajar con servicios CDC
  En este procedimiento se describe cómo usar la Consola de configuración del servicio CDC para preparar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de manera que funcione con servicios CDC de Oracle y para crear un nuevo servicio CDC.  
  
### <a name="to-work-with-cdc-services"></a>Para trabajar con servicios CDC  
  
1.  En el menú **Inicio** , seleccione **Configuración del servicio CDC para Oracle**.  
  
2.  En el panel izquierdo, seleccione **Local CDC Services** (Servicios CDC locales), el nivel raíz.  
  
3.  Realice una o ambas de las tareas siguientes:  
  
    -   **Preparar SQL Server**  
  
         Seleccione esta opción en el panel **Acciones** del lado derecho de la Consola de configuración del servicio CDC.  
  
         También puede hacer clic con el botón derecho en **Local CDC Services** (Servicios CDC locales) y seleccionar **Prepare SQL Server**(Preparar SQL Server).  
  
         Se abrirá el cuadro de diálogo Preparando instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC de Oracle.  
  
         Para preparar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para los servicios CDC de Oracle, el inicio de sesión debe tener un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el rol fijo de servidor `dbcreator` . Este inicio de sesión se emplea para crear la base de datos MSXDBCDC necesaria para agregar servicios CDC de Oracle y, después, instancias CDC de Oracle.  
  
         Para obtener información acerca de cómo usar este cuadro de diálogo, vea [Prepare SQL Server for CDC](prepare-sql-server-for-cdc.md). Para obtener información sobre cómo habilitar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC, vea [Cómo preparar SQL Server para CDC](how-to-prepare-sql-server-for-cdc.md).  
  
    -   **Crear un nuevo servicio CDC**  
  
         Haga clic en **Nuevo servicio** en el panel **Acciones** del lado derecho de la Consola de configuración del servicio CDC.  
  
         También puede hacer clic con el botón derecho en **Local CDC Services** (Servicios CDC locales) y seleccionar **Nuevo servicio**.  
  
         Se abrirá el cuadro de diálogo Nuevo servicio CDC de Oracle.  
  
         Para obtener información acerca de cómo usar este cuadro de diálogo, vea [Create and Edit an Oracle CDC Service](create-and-edit-an-oracle-cdc-service.md). Para obtener información acerca de cómo crear o editar un servicio CDC, vea [Cómo crear y editar un servicio CDC](how-to-create-and-edit-a-cdc-service.md).  
  
         El inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado por el servicio CDC de Oracle solo necesita ser miembro del rol fijo de servidor `public` ; no se necesita ningún otro privilegio. Pero, para crear el servicio CDC de Oracle, el inicio de sesión necesita tener permiso de escritura en la base de datos MSXDBCDC (por ejemplo, es necesario asignar el rol de base de datos **db_owner** al inicio de sesión). Cuando un inicio de sesión sin permiso de escritura para la base de datos MSXDBDCDC intenta crear una nueva instancia CDC de Oracle, se muestra un mensaje de error. Haga clic en **Aceptar** en ese cuadro de diálogo para mostrar el cuadro de diálogo Conectar con SQL Server.  
  
         Para más información sobre cómo especificar las credenciales de un inicio de sesión que tenga permisos de escritura en la base de datos MSXDBCDC, como el rol de base de datos **db_owner** , vea [Crear y editar un servicio CDC de Oracle](create-and-edit-an-oracle-cdc-service.md) y [Conexión con SQL Server](connection-to-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con servicios CDC](work-with-cdc-services.md)  
  
  