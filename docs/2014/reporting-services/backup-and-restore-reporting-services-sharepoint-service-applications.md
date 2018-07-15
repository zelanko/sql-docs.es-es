---
title: Copia de seguridad y restauración de Reporting Services SharePoint Service aplicaciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: dfb4ed77-90e5-4273-b690-89a945508ed2
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0ad72399371d662ee8842dd7f9bf72ce5a72b6b1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37212575"
---
# <a name="backup-and-restore-reporting-services-sharepoint-service-applications"></a>Copias de seguridad y restauración de aplicaciones de servicio de SharePoint para Reporting Services
  Este tema se describe cómo hacer una copia de seguridad y restaurar una aplicación de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] mediante Administración central de SharePoint o PowerShell. El tema contiene:  
  
-   [Limitaciones y restricciones](#bkmk_Restrictions)  
  
-   [Copia de seguridad de la aplicación de servicio](#bkmk_backup)  
  
-   [Restauración de la aplicación de servicio](#bkmk_restore)  
  
##  <a name="bkmk_BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="bkmk_Restrictions"></a> Limitaciones y restricciones  
  
> [!NOTE]  
>  Se puede realizar una copia de seguridad y una restauración parciales de aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] mediante la funcionalidad de copia de seguridad y restauración de SharePoint. **Se requieren pasos adicionales** y los pasos se documentan en este tema. Actualmente, el proceso de copia de seguridad **no** realiza una copia de seguridad de las claves de cifrado ni de las credenciales para las cuentas de ejecución desatendidas (UEA) o con autenticación de Windows en la base de datos de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
###  <a name="bkmk_recommendations"></a> Recomendaciones  
  
-   Realice una copia de seguridad de las claves de cifrado antes de iniciar la copia de seguridad de SharePoint. Si no hace una copia de seguridad de las claves de cifrado, no podrá acceder a los datos cifrados después de restaurar la aplicación de servicio. Tendrá que eliminar los datos cifrados.  
  
-   Compruebe si su [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] aplicación de servicio utiliza UEA o Windows autenticación para el acceso a la base de datos. Si es así, compruebe cuáles son las credenciales correctas para poder configurar correctamente la aplicación de servicio después del proceso de restauración.  
  
-   Compruebe que el archivo de registro de copia de seguridad de SharePoint se crea en la misma carpeta que el archivo de copia de seguridad. El archivo se denomina normalmente **spbackup.log**  
  
##  <a name="bkmk_backup"></a> Copia de seguridad de la aplicación de servicio  
 Realice los pasos siguientes en el orden indicado:  
  
1.  Realice una copia de seguridad de las claves de cifrado.  
  
2.  Copia de seguridad de la aplicación de servicio  
  
3.  Compruebe si la aplicación de servicio utiliza UEA o la autenticación de Windows para acceder a la base de datos. Si es así, anote las credenciales para poder usarlas cuando configure la aplicación de servicio una vez restaurada.  
  
### <a name="backup-the-encryption-keys-using-central-administration"></a>Copia de seguridad de las claves de cifrado mediante Administración central  
 Para más información sobre cómo realizar copias de seguridad de las claves de cifrado de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , vea la sección "Claves de cifrado" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
###  <a name="bkmk_centraladmin"></a> Copia de seguridad de la aplicación de servicio mediante Administración central de SharePoint  
 Para realizar una copia de seguridad de la aplicación de servicio, siga estos pasos:  
  
1.  En Administración central de SharePoint, haga clic en **Realizar una copia de seguridad** en el grupo **Realizar copias de seguridad y restauración** .  
  
2.  En el nodo **Servicios compartidos** , expanda **Aplicaciones de servicios compartidos** y seleccione la aplicación de servicio. Tendrá un tipo de **Aplicación del servicio SQL Server Reporting Services**.  
  
3.  Haga clic en **Siguiente**.  
  
4.  Escriba la ruta de acceso en **Ubicación de copia de seguridad:** y haga clic en **Iniciar copia de seguridad**  
  
5.  Repita el proceso anterior, pero en lugar de seleccionar la aplicación de servicio, expanda el nodo **Servidores proxy de servicios compartidos** y seleccione el proxy de la aplicación de servicio. Tendrá un tipo de **Proxy de aplicación del servicio SQL Server Reporting Services**.  
  
 Para obtener más información, consulte los siguientes temas en la documentación de SharePoint:  
  
 [Copia de seguridad de una aplicación de servicio (SharePoint Foundation 2010) en la documentación de SharePoint](http://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Copia de seguridad de una aplicación de servicio (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Comprobación de la cuenta de ejecución y autenticación de la base de datos  
 **Cuenta de la ejecución:** para comprobar si la aplicación de servicio utiliza una cuenta de ejecución:  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio** .  
  
2.  Haga clic el nombre de la aplicación de servicio y después en **Administrar** en la cinta de opciones de SharePoint.  
  
3.  Haga clic en **Cuenta de ejecución**.  
  
4.  Si se configura una cuenta de ejecución, tendrá que conocer las credenciales cuando llegue el momento de restaurar una copia de seguridad de la aplicación de servicio. No realice el procedimiento de copia de seguridad y restauración hasta que sepa cuáles son las credenciales correctas.  
  
 **Autenticación de la base de datos:** para comprobar si la aplicación de servicio utiliza la Autenticación de Windows para la autenticación de la base de datos:  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio** .  
  
2.  Haga clic el nombre de la aplicación de servicio y después en **Propiedades** en la cinta de opciones de SharePoint.  
  
3.  Examine la sección **Base de datos del servicio Reporting Services (SSRS)** .  
  
4.  Si se configura la autenticación de Windows, necesita conocer las credenciales para poder configurar la aplicación de servicio una vez restaurada. No realice el procedimiento de copia de seguridad y restauración hasta que sepa cuáles son las credenciales correctas.  
  
##  <a name="bkmk_restore"></a> Restauración de la aplicación de servicio  
 Realice los pasos siguientes en el orden indicado:  
  
1.  Restaure la aplicación de servicio de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
2.  Restaure las claves de cifrado.  
  
3.  Si la aplicación de servicio utilizaba una cuenta de ejecución o la autenticación de Windows para el acceso a la base de datos, configure las credenciales.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restauración de la aplicación de servicio mediante Administración central de SharePoint  
  
1.  En Administración central de SharePoint, haga clic en **Restaurar de una copia de seguridad** en el grupo **Realizar copias de seguridad y restauración** .  
  
2.  Especifique la ruta de acceso del archivo de copia de seguridad en **Ubicación del directorio de copia de seguridad** y haga clic en **Actualizar**.  
  
3.  Seleccione la copia de seguridad de la aplicación de servicio en la lista **Componente principal** y después haga clic en **Siguiente**.  
  
4.  Seleccione su [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] aplicación y, a continuación, haga clic en **siguiente**.  
  
5.  En la sección **Nombres y contraseñas de inicio de sesión** , escriba la contraseña del nombre de inicio de sesión. El cuadro de nombre de inicio de sesión debe rellenarse con el inicio de sesión que usaba la aplicación de servicio antes de que se realizara la copia de seguridad.  
  
6.  Haga clic en **Iniciar restauración**.  
  
7.  Repita el proceso anterior, pero en lugar de restaurar la aplicación de servicio, expanda el nodo **Servicios compartidos** y después expanda el nodo **Aplicaciones de servicios compartidos** .  
  
 Para obtener más información, consulte los siguientes temas en la documentación de SharePoint:  
  
 [Restauración de una aplicación de servicio (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Restauración de una aplicación de servicio (SharePoint Server 2010)](ttp://technet.microsoft.com/library/ee428305.aspx).  
  
### <a name="restore-the-encryption-keys-using-central-administration"></a>Restauración de las claves de cifrado mediante Administración central  
 Para obtener información acerca de cómo restaurar la [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] claves de cifrado, vea la sección "Claves de cifrado" de [administrar una aplicación de servicio de Reporting Services SharePoint](../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).  
  
### <a name="configure-the-execution-account-and-database-authentication"></a>Configurar la cuenta de ejecución y la autenticación de la base de datos  
 **Cuenta de ejecución:** si la aplicación de servicio utilizaba una cuenta de ejecución, realice el procedimiento siguiente para configurarla:  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio** .  
  
2.  Haga clic el nombre de la aplicación de servicio y después en **Administrar** en la cinta de opciones de SharePoint.  
  
3.  Haga clic en **Cuenta de ejecución**.  
  
4.  Especifique la cuenta, la contraseña y active la casilla **Especificar una cuenta de ejecución** .  
  
5.  Haga clic en **Aceptar**.  
  
 **Autenticación de la base de datos:** si la aplicación de servicio utilizaba la autenticación de Windows para la autenticación de la base de datos, realice el procedimiento siguiente:  
  
1.  En Administración central de SharePoint, en el grupo **Administración de aplicaciones** , haga clic en **Administrar aplicaciones de servicio** .  
  
2.  Haga clic el nombre de la aplicación de servicio y después en **Propiedades** en la cinta de opciones de SharePoint.  
  
3.  Examine la sección **Base de datos del servicio Reporting Services (SSRS)** .  
  
4.  Seleccione **Autenticación de Windows**.  
  
5.  Escriba la cuenta y la contraseña. Seleccione **Usar como credenciales de Windows** si procede.  
  
6.  Haga clic en **Aceptar**.  
  
  
