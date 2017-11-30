---
title: "Copias de seguridad y restauración de aplicaciones de servicio de SharePoint de Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f127627402993c51c64ca3ccaa3a1791da210a53
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Copias de seguridad y restauración de aplicaciones de servicio de SharePoint de Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

En este tema se explica cómo hacer una copia de seguridad y restaurar una aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante Administración central de SharePoint o PowerShell.

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

## <a name="before-you-begin"></a>Antes de empezar

### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones

> [!NOTE]
>  Se puede realizar una copia de seguridad y una restauración parciales de aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] mediante la funcionalidad de copia de seguridad y restauración de SharePoint. **Se requieren pasos adicionales** y los pasos se documentan en este tema. Actualmente, el proceso de copia de seguridad **no** realiza una copia de seguridad de las claves de cifrado ni de las credenciales de las cuentas de ejecución desatendidas (UEA) o con autenticación de Windows en la base de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

### <a name="recommendations"></a>Recomendaciones
  
-   Realice una copia de seguridad de las claves de cifrado antes de iniciar la copia de seguridad de SharePoint. Si no hace una copia de seguridad de las claves de cifrado, no podrá acceder a los datos cifrados después de restaurar la aplicación de servicio. Tendrá que eliminar los datos cifrados.  
  
-   Compruebe si la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza UEA o la autenticación de Windows para acceder a la base de datos. Si es así, compruebe cuáles son las credenciales correctas para poder configurar correctamente la aplicación de servicio después del proceso de restauración.  
  
-   Compruebe que el archivo de registro de copia de seguridad de SharePoint se crea en la misma carpeta que el archivo de copia de seguridad. El archivo se denomina normalmente **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>Hacer una copia de seguridad de la aplicación de servicio

 Realice los pasos siguientes en el orden indicado:  
  
1.  Hacer una copia de seguridad de las claves de cifrado  
  
2.  Hacer una copia de seguridad de la aplicación de servicio  
  
3.  Compruebe si la aplicación de servicio utiliza UEA o la autenticación de Windows para acceder a la base de datos. Si es así, anote las credenciales para poder usarlas cuando configure la aplicación de servicio una vez restaurada.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Copia de seguridad de las claves de cifrado mediante Administración central de SharePoint

Para más información sobre cómo realizar copias de seguridad de las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea la sección "Claves de cifrado" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Copia de seguridad de la aplicación de servicio mediante Administración central de SharePoint

Para realizar una copia de seguridad de la aplicación de servicio, siga estos pasos:  
  
1.  En Administración central de SharePoint, seleccione **Realizar copia de seguridad** en el grupo **Copias de seguridad y restauración**.  
  
2.  En el nodo **Servicios compartidos** , expanda **Aplicaciones de servicios compartidos** y seleccione la aplicación de servicio. Tendrá un tipo de **Aplicación del servicio SQL Server Reporting Services**.  
  
3.  Seleccione **Siguiente**.  
  
4.  Escriba la ruta de acceso en **Ubicación de copia de seguridad:** y seleccione **Iniciar copia de seguridad**.  
  
5.  Repita el proceso anterior, pero en lugar de seleccionar la aplicación de servicio, expanda el nodo **Servidores proxy de servicios compartidos** y seleccione el proxy de la aplicación de servicio. Tendrá un tipo de **Proxy de aplicación del servicio SQL Server Reporting Services**.  
  
 Para obtener más información, consulte los siguientes temas en la documentación de SharePoint:  
  
 [Copia de seguridad de una aplicación de servicio (SharePoint Foundation 2010) en la documentación de SharePoint](http://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Copia de seguridad de una aplicación de servicio (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Comprobación de la cuenta de ejecución y autenticación de la base de datos

 **Cuenta de la ejecución:** para comprobar si la aplicación de servicio utiliza una cuenta de ejecución:  
  
1.  En Administración central de SharePoint, seleccione **Administrar aplicaciones de servicio** en el grupo **Administración de aplicaciones**.  
  
2.  Seleccione el nombre de la aplicación de servicio y después **Administrar** en la cinta de SharePoint.  
  
3.  Seleccione **Cuenta de ejecución**.  
  
4.  Si se configura una cuenta de ejecución, tendrá que conocer las credenciales cuando llegue el momento de restaurar una copia de seguridad de la aplicación de servicio. No realice el procedimiento de copia de seguridad y restauración hasta que sepa cuáles son las credenciales correctas.  
  
 **Autenticación de la base de datos:** para comprobar si la aplicación de servicio utiliza la Autenticación de Windows para la autenticación de la base de datos:  
  
1.  En Administración central de SharePoint, seleccione **Administrar aplicaciones de servicio** en el grupo **Administración de aplicaciones**.  
  
2.  Seleccione el nombre de la aplicación de servicio y después **Propiedades** en la cinta de SharePoint.  
  
3.  Examine la sección **Base de datos del servicio Reporting Services (SSRS)** .  
  
4.  Si se configura la autenticación de Windows, necesita conocer las credenciales para poder configurar la aplicación de servicio una vez restaurada. No realice el procedimiento de copia de seguridad y restauración hasta que sepa cuáles son las credenciales correctas.  
  
## <a name="restore-the-service-application"></a>Restauración de la aplicación de servicio

 Realice los pasos siguientes en el orden indicado:  
  
1.  Restaure la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Restaure las claves de cifrado.  
  
3.  Si la aplicación de servicio utilizaba una cuenta de ejecución o la autenticación de Windows para el acceso a la base de datos, configure las credenciales.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restauración de la aplicación de servicio mediante Administración central de SharePoint
  
1.  En Administración central de SharePoint, seleccione **Restaurar a partir de una copia de seguridad** en el grupo **Copias de seguridad y restauración**.  
  
2.  Especifique la ruta de acceso del archivo de copia de seguridad en **Ubicación del directorio de copia de seguridad** y seleccione **Actualizar**.  
  
3.  Seleccione la copia de seguridad de la aplicación de servicio en la lista **Componente superior** y después **Siguiente**.  
  
4.  Seleccione la aplicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y luego **Siguiente**.  
  
5.  En la sección **Nombres y contraseñas de inicio de sesión** , escriba la contraseña del nombre de inicio de sesión. El cuadro de nombre de inicio de sesión debe rellenarse con el inicio de sesión que usaba la aplicación de servicio antes de que se realizara la copia de seguridad.  
  
6.  Seleccione **Iniciar restauración**.  
  
7.  Repita el proceso anterior, pero en lugar de restaurar la aplicación de servicio, expanda el nodo **Servicios compartidos** y después expanda el nodo **Aplicaciones de servicios compartidos** .  
  
 Para obtener más información, consulte los siguientes temas en la documentación de SharePoint:  
  
 [Restauración de una aplicación de servicio (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Restauración de una aplicación de servicio (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx).  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Restauración de las claves de cifrado mediante Administración central de SharePoint

 Para más información sobre la restauración de las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea la sección "Claves de cifrado" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Configuración de la cuenta de ejecución y la autenticación de base de datos

 **Cuenta de ejecución:** si la aplicación de servicio utilizaba una cuenta de ejecución, realice el procedimiento siguiente para configurarla:  
  
1.  En Administración central de SharePoint, seleccione **Administrar aplicaciones de servicio** en el grupo **Administración de aplicaciones**.  
  
2.  Seleccione el nombre de la aplicación de servicio y después **Administrar** en la cinta de SharePoint.  
  
3.  Seleccione **Cuenta de ejecución**.  
  
4.  Especifique la cuenta, la contraseña y active la casilla **Especificar una cuenta de ejecución** .  
  
5.  Seleccione **Aceptar**.  
  
 **Autenticación de la base de datos:** si la aplicación de servicio utilizaba la autenticación de Windows para la autenticación de la base de datos, realice el procedimiento siguiente:  
  
1.  En Administración central de SharePoint, seleccione **Administrar aplicaciones de servicio** en el grupo **Administración de aplicaciones**.  
  
2.  Seleccione el nombre de la aplicación de servicio y después **Propiedades** en la cinta de SharePoint.  
  
3.  Examine la sección **Base de datos del servicio Reporting Services (SSRS)** .  
  
4.  Seleccione **Autenticación de Windows**.  
  
5.  Escriba la cuenta y la contraseña. Seleccione **Usar como credenciales de Windows** si procede.  
  
6.  Seleccione **Aceptar**.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
