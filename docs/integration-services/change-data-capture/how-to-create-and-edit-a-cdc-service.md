---
title: "Cómo crear y editar un servicio CDC | Documentos de Microsoft"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1b3d47a5-dc89-482d-bbc7-fff04f194c43
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: daf64f88220832573485701883921ad575e789bc
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="how-to-create-and-edit-a-cdc-service"></a>Cómo crear y editar un servicio CDC
  En estos procedimientos se describe cómo crear y editar un nuevo servicio CDC de Oracle desde la Consola de configuración del servicio CDC.  
  
 Para poder realizar este procedimiento, un usuario de Windows debe tener privilegios de administrador en el equipo donde está configurado el servicio CDC de Oracle.  
  
### <a name="to-create-a-new-cdc-service"></a>Para crear un nuevo servicio CDC  
  
1.  En el menú **Inicio** , seleccione **Configuración del servicio CDC para Oracle**.  
  
2.  En el panel izquierdo, haga clic con el botón secundario en Servicios CDC locales y seleccione Nuevo servicio.  
  
     También puede hacer clic en **Nuevo servicio** en el panel **Acciones** .  
  
3.  Escriba la información necesaria en el cuadro de diálogo Nuevo servicio CDC de Oracle. Vea [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) para obtener información acerca de cómo especificar información en el cuadro de diálogo Nuevo servicio CDC de Oracle.  
  
     El servicio CDC de Oracle emplea el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporcionado en el cuadro de diálogo Nuevo servicio CDC de Oracle cuando se ejecuta. Este inicio de sesión solo necesita ser miembro del rol fijo de servidor public; no se necesita ningún otro privilegio. Una vez agregadas nuevas instancias CDC de Oracle, ese inicio de sesión recibe acceso **db_owner** a las bases de datos CDC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociadas.  
  
4.  Cuando termine de especificar la información necesaria, haga clic en **Aceptar**.  
  
     Para crear la definición del servicio de Windows CDC de Oracle, el programa necesita acceso de actualización a la base de datos MSXDBCDC en la instancia asociada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Al hacer clic en **Aceptar**, un cuadro de diálogo pide al usuario que especifique un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un acceso de actualización para la base de datos MSXDBCDC.  
  
     Para obtener información acerca de los datos que debe escribir en el cuadro de diálogo Conectar con SQL Server, vea [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo Nuevo servicio CDC de Oracle.  
  
### <a name="to-edit-a-cdc-service"></a>Para editar un servicio CDC  
  
1.  En el menú **Inicio** , seleccione **Configuración del servicio CDC para Oracle**.  
  
2.  En el panel izquierdo, seleccione **Servicios CDC locales** , haga clic con el botón derecho en el servicio local que quiera editar y seleccione **Propiedades**.  
  
     También puede seleccionar el servicio con el que está trabajando en la parte central y a continuación, en el panel **Acciones** , hacer clic en **Propiedades**.  
  
3.  Escriba la información necesaria en el cuadro de diálogo Propiedades del servicio CDC. Vea [Create and Edit an Oracle CDC Service](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md) para obtener información acerca de cómo especificar información en el cuadro de diálogo Propiedades del servicio CDC.  
  
4.  Cuando termine de escribir la información necesaria, haga clic en **Aceptar**; se abrirá el cuadro de diálogo Conectar con SQL Server.  
  
     Cuando un inicio de sesión sin permiso de escritura para la base de datos MSXDBDCDC intenta crear una nueva instancia CDC de Oracle, se muestra un mensaje de error. Haga clic en **Aceptar** en ese cuadro de diálogo para mostrar el cuadro de diálogo Conectar con SQL Server. En este cuadro de diálogo debe especificar las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como el rol de base de datos **db_owner** .  
  
     Para obtener información acerca de los datos que debe escribir en el cuadro de diálogo Conectar con SQL Server, vea [Connection to SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md).  
  
5.  Haga clic en **Aceptar** en el cuadro de diálogo Conectar con Oracle. Se cerrarán ambos cuadros de diálogo, y se actualizará y registrará el servicio.  
  
## <a name="see-also"></a>Vea también  
 [Diseñador de captura de datos modificados para Oracle de Attunity](../../integration-services/change-data-capture/change-data-capture-designer-for-oracle-by-attunity.md)   
 [Crear y editar un servicio CDC de Oracle](../../integration-services/change-data-capture/create-and-edit-an-oracle-cdc-service.md)  
  
  
