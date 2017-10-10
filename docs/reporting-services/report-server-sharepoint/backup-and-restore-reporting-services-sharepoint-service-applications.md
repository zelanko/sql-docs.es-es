---
title: Copia de seguridad y restaurar las aplicaciones de servicio de SharePoint de Reporting Services | Documentos de Microsoft
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
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: b6dcd64d6f9662ae592474053e6cc9bbce53a83e
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Copia de seguridad y restaurar las aplicaciones de servicio de SharePoint de Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Este tema describe cómo realizar copias de y restaurar un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicación services mediante Administración Central de SharePoint o PowerShell.

> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

## <a name="before-you-begin"></a>Antes de empezar

### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones

> [!NOTE]
>  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]parcialmente posible copia de seguridad y restaurar aplicaciones de servicio con SharePoint de copia de seguridad y restaurar la funcionalidad. **Se requieren pasos adicionales** y los pasos se documentan en este tema. Actualmente el proceso de copia de seguridad **no** copia de seguridad de las claves de cifrado y las credenciales de cuentas de ejecución desatendida (UEA) o la autenticación de windows para el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] base de datos.

### <a name="recommendations"></a>Recomendaciones
  
-   Hacer copia de seguridad de las claves de cifrado antes de iniciar la copia de seguridad de SharePoint. Si no copia las claves de cifrado, a continuación, no podrá tener acceso a los datos cifrados, la restauración de la aplicación de servicio. Tendrá que eliminar los datos cifrados.  
  
-   Compruebe si la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza UEA o la autenticación de Windows para acceder a la base de datos. Si es así, compruebe cuáles son las credenciales correctas para poder configurar correctamente la aplicación de servicio después del proceso de restauración.  
  
-   Revise que el registro de copia de seguridad de SharePoint se crea en la misma carpeta que el archivo de copia de seguridad. El archivo se denomina normalmente **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>Hacer copia de seguridad de la aplicación de servicio

 Realice los pasos siguientes en el orden indicado:  
  
1.  Hacer copia de seguridad de las claves de cifrado  
  
2.  Hacer copia de seguridad de la aplicación de servicio  
  
3.  Compruebe si la aplicación de servicio utiliza UEA o la autenticación de Windows para acceder a la base de datos. Si es así, anote las credenciales para poder usarlas cuando configure la aplicación de servicio una vez restaurada.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Hacer copia de seguridad de las claves de cifrado mediante Administración Central de SharePoint

Para más información sobre cómo realizar copias de seguridad de las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea la sección "Claves de cifrado" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Hacer copia de seguridad de la aplicación de servicio mediante Administración Central de SharePoint

Para realizar una copia de seguridad de la aplicación de servicio, siga estos pasos:  
  
1.  En, seleccione Administración Central de SharePoint **realizar una copia de seguridad** en el **de copia de seguridad y restauración** grupo.  
  
2.  En el nodo **Servicios compartidos** , expanda **Aplicaciones de servicios compartidos** y seleccione la aplicación de servicio. Tendrá un tipo de **Aplicación del servicio SQL Server Reporting Services**.  
  
3.  Seleccione **Siguiente**.  
  
4.  Escriba la ruta de acceso para la **ubicación de copia de seguridad:** y seleccione **iniciar copia de seguridad**  
  
5.  Repita el proceso anterior, pero en lugar de seleccionar la aplicación de servicio, expanda el nodo **Servidores proxy de servicios compartidos** y seleccione el proxy de la aplicación de servicio. Tendrá un tipo de **Proxy de aplicación del servicio SQL Server Reporting Services**.  
  
 Para obtener más información, consulte los siguientes temas en la documentación de SharePoint:  
  
 [Copia de seguridad de una aplicación de servicio (SharePoint Foundation 2010) en la documentación de SharePoint](http://msdn.microsoft.com/library/ee748601.aspx).  
  
 [Copia de seguridad de una aplicación de servicio (SharePoint Server 2010)](http://technet.microsoft.com/library/ee428318.aspx)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Comprobar la autenticación de base de datos y la cuenta de ejecución

 **Cuenta de la ejecución:** para comprobar si la aplicación de servicio utiliza una cuenta de ejecución:  
  
1.  En Administración Central de SharePoint, seleccione **administrar aplicaciones de servicio** en el **Application Management** grupo.  
  
2.  Seleccione el nombre de la aplicación de servicio y, a continuación, seleccione **administrar** en la cinta de opciones de SharePoint.  
  
3.  Seleccione **cuenta de ejecución**.  
  
4.  Si se configura una cuenta de ejecución, tendrá que conocer las credenciales cuando llegue el momento de restaurar una copia de seguridad de la aplicación de servicio. No realice el procedimiento de copia de seguridad y restauración hasta que sepa cuáles son las credenciales correctas.  
  
 **Autenticación de la base de datos:** para comprobar si la aplicación de servicio utiliza la Autenticación de Windows para la autenticación de la base de datos:  
  
1.  En Administración Central de SharePoint, seleccione **administrar aplicaciones de servicio** en el **Application Management** grupo.  
  
2.  Seleccione el nombre de la aplicación de servicio y, a continuación, seleccione **propiedades** en la cinta de opciones de SharePoint.  
  
3.  Examine la sección **Base de datos del servicio Reporting Services (SSRS)** .  
  
4.  Si se configura la autenticación de Windows, necesita conocer las credenciales para poder configurar la aplicación de servicio una vez restaurada. No realice el procedimiento de copia de seguridad y restauración hasta que sepa cuáles son las credenciales correctas.  
  
## <a name="restore-the-service-application"></a>Restauración de la aplicación de servicio

 Realice los pasos siguientes en el orden indicado:  
  
1.  Restaure la aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Restaure las claves de cifrado.  
  
3.  Si la aplicación de servicio utilizaba una cuenta de ejecución o la autenticación de Windows para el acceso a la base de datos, configure las credenciales.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restauración de la aplicación de servicio mediante Administración Central de SharePoint
  
1.  En, seleccione Administración Central de SharePoint **restaurar a partir de una copia de seguridad** en el **de copia de seguridad y restauración** grupo.  
  
2.  Escriba la ruta de acceso al archivo de copia de seguridad en **ubicación del directorio de copia de seguridad** cuadro y seleccione **actualizar**.  
  
3.  Seleccione la copia de seguridad de aplicación de servicio desde el **componente principal** lista y, a continuación, seleccione **siguiente**.  
  
4.  Seleccione el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] aplicación y, a continuación, seleccione **siguiente**.  
  
5.  En la sección **Nombres y contraseñas de inicio de sesión** , escriba la contraseña del nombre de inicio de sesión. El cuadro de nombre de inicio de sesión se debe rellenar con el inicio de sesión de que la aplicación de servicio utilizaba antes de la copia de seguridad.  
  
6.  Seleccione **Iniciar restauración**.  
  
7.  Repita el proceso anterior, pero en lugar de restaurar la aplicación de servicio, expanda el nodo **Servicios compartidos** y después expanda el nodo **Aplicaciones de servicios compartidos** .  
  
 Para obtener más información, consulte los siguientes temas en la documentación de SharePoint:  
  
 [Restauración de una aplicación de servicio (SharePoint Foundation 2010)](http://msdn.microsoft.com/library/ee748615.aspx).  
  
 [Restauración de una aplicación de servicio (SharePoint Server 2010)](https://technet.microsoft.com/library/ee428305.aspx).  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Restaurar las claves de cifrado mediante Administración Central de SharePoint

 Para más información sobre la restauración de las claves de cifrado de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea la sección "Claves de cifrado" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Configurar la autenticación de base de datos y la cuenta de ejecución

 **Cuenta de ejecución:** si la aplicación de servicio utilizaba una cuenta de ejecución, realice el procedimiento siguiente para configurarla:  
  
1.  En Administración Central de SharePoint, seleccione **administrar aplicaciones de servicio** en el **Application Management** grupo.  
  
2.  Seleccione el nombre de la aplicación de servicio y, a continuación, seleccione **administrar** en la cinta de opciones de SharePoint.  
  
3.  Seleccione **cuenta de ejecución**.  
  
4.  Especifique la cuenta, la contraseña y active la casilla **Especificar una cuenta de ejecución** .  
  
5.  Seleccione **Aceptar**.  
  
 **Autenticación de la base de datos:** si la aplicación de servicio utilizaba la autenticación de Windows para la autenticación de la base de datos, realice el procedimiento siguiente:  
  
1.  En, seleccione Administración Central de SharePoint **administrar aplicaciones de servicio** en el **Application Management** grupo.  
  
2.  Seleccione el nombre de la aplicación de servicio y, a continuación, seleccione **propiedades** en la cinta de opciones de SharePoint.  
  
3.  Examine la sección **Base de datos del servicio Reporting Services (SSRS)** .  
  
4.  Seleccione **Autenticación de Windows**.  
  
5.  Escriba la cuenta y la contraseña. Seleccione **Usar como credenciales de Windows** si procede.  
  
6.  Seleccione **Aceptar**

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
