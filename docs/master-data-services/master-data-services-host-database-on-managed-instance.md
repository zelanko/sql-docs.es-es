---
title: Base de datos host en una instancia administrada | Microsoft Docs
description: Describe cómo configurar una base de datos de MDS en una instancia administrada de.
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0081ea193452e4e92938051bc7b4a40bc8631eaa
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155379"
---
# <a name="host-database-on-managed-instance"></a>Base de datos host en instancia administrada

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este artículo se explica cómo configurar una base de datos de MDS en una instancia administrada.
  
## <a name="preparation"></a>Preparación

Necesitamos finalizar los pasos siguientes en la preparación.
- Finalizar la creación y configuración de la instancia administrada. Incluir red virtual y VPN de punto a sitio.
- Finalizar la configuración de la máquina de aplicación Web.
  - Incluye la VPN de punto a sitio de instalación.
  - Instalar roles y características.

**Lado de la base de datos:**

1. Crear una instancia administrada de Azure SQL Database incluye una red virtual. [Inicio rápido: Crear una instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)
2. Configure una conexión de punto a sitio. [Configuración de una conexión de punto a sitio a una red virtual mediante la autenticación de certificados de Azure nativa: Azure Portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
3. Configurar la autenticación de Azure Active Directory con SQL Database instancia administrada. [Configuración y administración de la autenticación de Azure Active Directory con SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)

**Lado del equipo de la aplicación web:**

1. Instale el certificado de conexión de punto a sitio y VPN para asegurarse de que la máquina puede acceder a SQL Database instancia administrada. [Configuración de una conexión de punto a sitio a una red virtual mediante la autenticación de certificados de Azure nativa: Azure Portal](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
2. Instale el rol y las características. Se requiere la siguiente característica.

- Roles

      Internet Information Services
      Web Management Tools
      IIS Management Console
      World Wide Web Services
      Application Development
      .NET Extensibility 3.5
      .NET Extensibility 4.5
      ASP.NET 3.5
      ASP.NET 4.5
      ISAPI Extensions
      ISAPI Filters
      Common HTTP Features
      Default Document
      Directory Browsing
      HTTP Errors
      Static Content
      [Note: Do not install WebDAV Publishing]
      Health and Diagnostics
      HTTP Logging
      Request Monitor
      Performance
      Static Content Compression
      Security
      Request Filtering
      Windows Authentication

- Características:

      .NET Framework 3.5 (includes .NET 2.0 and 3.0)
      .NET Framework 4.5 Advanced Services
      ASP.NET 4.5
      WCF Services
      HTTP Activation [Note: This is required.]
      TCP Port Sharing
      Windows Process Activation Service
      Process Model
      .NET Environment
      Configuration APIs
      Dynamic Content Compression

## <a name="install-and-configure-includessmdsshort_mdincludesssmdsshort-mdmd-web-application"></a>Instalación y configuración [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] de una aplicación Web

Necesitamos finalizar los pasos siguientes para instalar y configurar [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)].

1. Instale la característica de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] inclusión de SQL Server 2019.
2. Cree una [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] base de datos en la instancia de administración.
3. Cree y configure la aplicación [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]web para.
  
**Instalación de SQL Server 2019**

Use el Asistente para la instalación de SQL Server o el símbolo del sistema [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]para instalar.

1. Haga doble clic en Setup.exe y siga los pasos del asistente para la instalación.

2. Seleccione [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en la página selección de características en características compartidas.
Esto instala [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], ensamblados, un complemento de Windows PowerShell y carpetas y archivos para las aplicaciones y los servicios web.

    ![MDS-SQLServer2019-config-mi-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "MDS-SQLServer2019-config-MI_SQLFeatureSelection")  

**Configurar la base de datos y el sitio web**

1. Conecte el Virtual Network de Azure para asegurarse de que puede conectarse a la instancia administrada.

    ![MDS-SQLServer2019-config-mi-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "MDS-SQLServer2019-config-MI_P2SVPNConnect")  

2. Inicie el [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Y haga clic en **configuración de base de datos** en el panel izquierdo.

3. Haga clic en **crear base de datos**y, a continuación, haga clic en siguiente en el Asistente para **crear bases de datos** .

4. En la página **servidor de base de datos** , rellene la instancia de **SQL Server** , seleccione el **tipo de autenticación** y, después, haga clic en conexión de **prueba** para confirmar que puede conectarse a la base de datos con las credenciales del tipo de autenticación que seleccionadas. Haga clic en Siguiente.

   > [!NOTE]
   > - Instancia de SQL Server para la instancia administrada como "xxxxxxx.xxxxxxx.database.windows.net"
   > - En el caso de la instancia administrada, se admite el tipo de autenticación " **SQL Server cuenta"** y **"usuario actual – Active Directory integrado"** .
   > - Al seleccionar **usuario actual: Active Directory integrado** como tipo de autenticación, el cuadro **nombre de usuario** es de solo lectura y muestra el nombre de la cuenta de usuario de Windows que ha iniciado sesión en el equipo. Si está ejecutando SQL Server 2019 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] en una máquina virtual (VM) de Azure, el cuadro Nombre de **usuario** muestra el nombre de la máquina virtual y el nombre de usuario de la cuenta de administrador local en la máquina virtual.

    Asegúrese de que la autenticación contiene la regla **"sysadmin"** para la instancia administrada.
![MDS-SQLServer2019-config-mi-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "MDS-SQLServer2019-config-MI_CreateDBConnect")  

5. Escriba un nombre en el campo **Nombre de la base de datos** . Opcionalmente, para seleccionar una intercalación de Windows, desmarque la casilla **Intercalación predeterminada de SQL Server** y haga clic en una o varias de las opciones disponibles, como **Distinguir mayúsculas de minúsculas**. Haga clic en **Next**.

    ![MDS-SQLServer2019-config-mi-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "MDS-SQLServer2019-config-MI_CreatedDBName")  

6. En el campo **nombre de usuario** , especifique la cuenta de Windows del usuario que será el superusuario predeterminado para [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. Un superusuario tiene acceso a todas las áreas funcionales y puede agregar, eliminar y actualizar todos los modelos.

    ![MDS-SQLServer2019-config-mi-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "MDS-SQLServer2019-config-MI_createDBUserName")

7. Haga clic en **Siguiente** para ver un resumen de la configuración de la base de datos de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] y, luego, haga clic en **Siguiente** para crear la base de datos. Aparecerá la página **Avanzar y finalizar**.

8. Cuando se haya creado y configurado la base de datos, haga clic en **Finalizar**.

    Para obtener más información acerca de la configuración del **Asistente para crear bases de datos**, vea [Asistente para &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] crear bases&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md)de datos Configuration Manager.

9. En la página **configuración de base** de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]datos de la, haga clic en **Seleccionar base de datos**.

10. Haga clic en **conectar**, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] seleccione la base de datos creada en el paso 8 y, a continuación, haga clic en **Aceptar**.

    ![MDS-SQLServer2019-config-mi-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_connectDBName")

11. En [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], haga clic en **Configuración web** en el panel izquierdo.

12. En el cuadro de lista **Sitio web** , haga clic en **Sitio web predeterminado**y, luego, haga clic en **Crear** para crear una aplicación web.
![MDS-SQLServer2019-config-mi-Webconfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "MDS-SQLServer2019-config-MI_WebConfiguration")

   > [!NOTE] 
   > Al seleccionar **Sitio web predeterminado**, debe crear una aplicación web. Si selecciona **Crear nuevo sitio web** en el cuadro de lista, la aplicación se crea de forma automática.

    

13. En la sección **grupo de aplicaciones** , escriba un nombre de usuario diferente, escriba la contraseña y, a continuación, haga clic en Aceptar.
![MDS-SQLServer2019-config-mi-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "MDS-SQLServer2019-config-MI_CreateWebApplication")

   > [!NOTE]
   > Debe asegurarse de que el usuario puede tener acceso a la base de datos con Active Directory autenticación integrada que acaba de crear. O bien, debe cambiar la conexión en el archivo Web. config más adelante.

    

14. Para obtener más información sobre el cuadro de diálogo **crear aplicación web** , vea [ &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] cuadro de diálogo crear&#41;aplicación web Configuration Manager](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).

15. En la página **configuración Web** del cuadro **aplicación web** , haga clic en la aplicación que ha creado y, a continuación, haga clic en **seleccionar** en la sección **asociar aplicación con base de datos** .

16. Haga clic en **Conectar**, seleccione la base de datos de [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] que quiera asociar a la aplicación web y, después, haga clic en **Aceptar**.

    Ha terminado de configurar el sitio web. La página **configuración Web** muestra ahora el sitio Web seleccionado, la aplicación web que creó y la [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] base de datos asociada a la aplicación.

    ![MDS-SQLServer2019-config-mi-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "MDS-SQLServer2019-config-MI_WebConfigSelectDB")

17. Haga clic en **Aplicar**. Aparecerá el cuadro de mensaje **Configuración completada**. Haga clic en **Aceptar** en el cuadro de mensaje para iniciar la aplicación web. La dirección del sitio Web http://server es nombre/aplicación Web/.

## <a name="other-authentication-type-to-connect-managed-instance-database-on-web-application"></a>Otro tipo de autenticación para conectar la base de datos de instancia administrada en la aplicación Web

Podemos obtener el archivo **Web. config** en C:\Archivos de Programa\microsoft SQL Server\150\Master Data Services\WebApplication. Podemos modificar la connectionString para cambiar otro tipo de autenticación para conectar la base de datos de instancia administrada.

El tipo de autenticación predeterminado es "**Active Directory integrado**", que sigue la cadena de conexión de ejemplo.

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
```

También se admite la autenticación Active Directory contraseña y la autenticación de SQL Server. a continuación, se muestra la cadena de conexión de ejemplo.

Autenticación de contraseña de Active Directory

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
```

Autenticación de SQL Server

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-database-version"></a>Actualización [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] y versión de la base de datos

**Actualización[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]**

Instale la **actualización acumulativa**de SQL Server 2019, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] que se actualizará automáticamente.

**Actualizar versión de base de datos**

Si recibe el error "la versión del cliente es incompatible con la versión de la base de datos" después de instalar la **actualización acumulativa**de SQL Server 2019, debe actualizar la versión de la base de datos.

![MDS-SQLServer2019-config-mi-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "MDS-SQLServer2019-config-MI_UpgradeDBPage")

1. Inicie el [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. Y haga clic en **configuración de base de datos** en el panel izquierdo.

2. En la página **configuración de base** de [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]datos de la, haga clic en **Seleccionar base de datos**.

3. Haga clic en **conectar**, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] seleccione la base de datos asociada a la aplicación web y, a continuación, haga clic en **Aceptar**.

    ![MDS-SQLServer2019-config-mi-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_ConnectDBName")

4. Haga clic en **Actualizar base de datos...** botón

    ![MDS-SQLServer2019-config-mi-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "MDS-SQLServer2019-config-MI_SelectUpgradeDB")

5. En el Asistente para actualizar base de datos, haga clic en el botón **siguiente** en la página de **bienvenida** y en la página **revisión de actualización** .

    ![MDS-SQLServer2019-config-mi-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "MDS-SQLServer2019-config-MI_UpgradeDBWizard")

6. Haga clic en el botón **Finalizar** cuando se complete toda la tarea.

## <a name="see-also"></a>Vea también

 [Master Data Services base de datos](../master-data-services/master-data-services-database.md) [Master Data Manager aplicación web](../master-data-services/master-data-manager-web-application.md) [Página &#40;configuración de base&#41; de datos administrador de configuración de Master Data Services](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md) [Novedades de Master Data Services &#40;MDS&#41; ](../master-data-services/what-s-new-in-master-data-services-mds.md)
