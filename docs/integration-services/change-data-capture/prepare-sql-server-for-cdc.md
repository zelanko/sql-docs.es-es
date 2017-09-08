---
title: Preparar SQL Server para CDC | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- prepSqlSrv
ms.assetid: 20b51dbf-a545-4234-87ae-4228268a0fb2
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 29eee5c85a323e70dab3ac9bdb25bd72820b0489
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="prepare-sql-server-for-cdc"></a>Preparar SQL Server para CDC
  El servicio CDC de Oracle necesita que todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contengan la base de datos MSXDBCDC. Esta base de datos se crea mediante la acción Preparar SQL Server de la Consola de configuración del servicio CDC. Esto crea un script especial que se ejecuta para crear las tablas, los procedimientos almacenados y otros artefactos necesarios para esta base de datos. Esta tarea solo se realiza una vez para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Para obtener más información acerca de la base de datos MSXDBCDC, vea La base de datos MSXDBCDC.  
  
 En la Consola de configuración del servicio CDC, haga clic en **Preparar SQL Server**. Si esta opción no está disponible, asegúrese de que esté seleccionado **Servicios CDC locales** en el panel izquierdo de la consola.  
  
## <a name="options"></a>Opciones  
  
### <a name="server-name"></a>Nombre de servidor  
 Escriba el nombre del servidor donde se encuentra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="authentication"></a>Autenticación  
 Seleccione una de las opciones siguientes:  
  
-   **Autenticación de Windows**  
  
-   **Autenticación de SQL Server**: si selecciona esta opción, debe escribir el **Nombre de usuario** y la **Contraseña** del usuario del servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que se está conectando.  
  
 Para preparar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para CDC de Oracle, el inicio de sesión debe tener permiso de escritura para la base de datos MSXDBCDC. Escriba las credenciales para un inicio de sesión que tenga permiso de escritura para la base de datos MSXDBCDC, como un miembro del rol `sysasmin` .  
  
### <a name="options"></a>Opciones  
 Haga clic en la flecha para ver las opciones disponibles que se pueden configurar. Puede elegir dejar estas opciones con el valor predeterminado. Las opciones disponibles son:  
  
-   **Tiempo de espera de la conexión**: escriba el tiempo (en segundos) que el servicio CDC para Oracle espera para establecer una conexión con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de agotarse el tiempo de espera. El valor predeterminado es **15**.  
  
-   **Tiempo de espera de ejecución**: escriba el tiempo (en segundos) que el servicio de Windows CDC de Oracle espera la ejecución de un comando antes de agotarse el tiempo de espera. El valor predeterminado es **30**.  
  
-   **Cifrar conexión**: seleccione **Cifrar conexión** para que la comunicación entre el servicio CDC de Oracle y la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino se realice mediante una conexión cifrada.  
  
-   **Avanzadas**: escriba cualquier propiedad de conexión adicional, si es necesario.  
  
### <a name="view-script"></a>Ver script  
 Haga clic en **Ver script** para ver una versión de solo lectura del script de configuración. Un administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar este script en la consola de administración de SQL Server para editarlo, si es necesario. Para obtener más información sobre el script para preparar SQL Server, vea [Preparar SQL Server para CDC de Oracle (Ver script)](../../integration-services/change-data-capture/prepare-sql-server-for-oracle-cdc-view-script.md).  
  
## <a name="see-also"></a>Vea también  
 [Cómo trabajar con servicios CDC](../../integration-services/change-data-capture/how-to-work-with-cdc-services.md)   
 [Cómo preparar SQL Server para CDC](../../integration-services/change-data-capture/how-to-prepare-sql-server-for-cdc.md)  
  
  
