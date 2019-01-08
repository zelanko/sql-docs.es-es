---
title: Preparar SQL Server para CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- prepSqlSrv
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e52f15a66c858aa1a04826f69342ba6a9dcd687e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804856"
---
# <a name="prepare-sql-server-for-cdc"></a>Preparar SQL Server para CDC
  El servicio CDC de Oracle necesita que todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contengan la base de datos MSXDBCDC. Esta base de datos se crea mediante la acción Preparar SQL Server de la Consola de configuración del servicio CDC. Esto crea un script especial que se ejecuta para crear las tablas, los procedimientos almacenados y otros artefactos necesarios para esta base de datos. Esta tarea solo se realiza una vez para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Para obtener más información acerca de la base de datos MSXDBCDC, vea La base de datos MSXDBCDC.  
  
 En la Consola de configuración del servicio CDC, haga clic en **Preparar SQL Server**. Si esta opción no está disponible, asegúrese de que esté seleccionado **Servicios CDC locales** en el panel izquierdo de la consola.  
  
## <a name="options"></a>Opciones  
  
### <a name="server-name"></a>Nombre del servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: Si selecciona esta opción, debe escribir el **nombre de usuario** y **contraseña** para el usuario en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se conecta.  
  
 Para preparar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC de Oracle, el inicio de sesión debe tener permiso de escritura para la base de datos MSXDBCDC. Escriba las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como un miembro del rol `sysasmin` .  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de conexión**: Escriba el tiempo (en segundos) que el servicio CDC para Oracle espera una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: Escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera que se ejecute un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: Seleccione **cifrar conexión** para la comunicación entre el servicio CDC de Oracle y el destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia mediante una conexión cifrada.  
  
-   **Avanzadas**: Escriba cualquier propiedad de conexión adicional, si es necesario.  
  
### <a name="view-script"></a>Ver script  
 Haga clic en **Ver script** para ver una versión de solo lectura del script de configuración. Un administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar este script en la consola de administración de SQL Server para editarlo, si es necesario. Para obtener más información sobre el script para preparar SQL Server, vea [Preparar SQL Server para CDC de Oracle (Ver script)](prepare-sql-server-for-oracle-cdc-view-script.md).  
  
## <a name="see-also"></a>Vea también  
 [Cómo trabajar con servicios CDC](work-with-cdc-services.md)   
 [Cómo preparar SQL Server para CDC](prepare-sql-server-for-cdc.md)  
  
  
