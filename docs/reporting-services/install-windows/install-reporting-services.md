---
title: Instalar SQL Server Reporting Services | Documentos de Microsoft
ms.date: 10/10/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 52c2f8fae79884b025e067b7d628cd3154ba93f4
ms.openlocfilehash: 5ce83ff18d6908441a3eaaf05599068ec5876308
ms.contentlocale: es-es
ms.lasthandoff: 10/10/2017

---
# <a name="install-sql-server-reporting-services"></a>Instalar SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

Instalación de SQL Server Reporting Services implica componentes de servidor para almacenar elementos de informe, informes de representación y procesamiento de suscripciones y otros servicios de informes.  Obtenga información acerca de cómo instalar el servidor de informes de Power BI.

Para descargar SQL Server 2017 Reporting Services, vaya a la [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55252).

> [!NOTE]
> ¿Busca el servidor de informes de BI de energía? Vea [instalar servidor de informes de BI de energía](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).

## <a name="before-you-begin"></a>Antes de empezar

Antes de instalar Reporting Services, revise la [requisitos de Hardware y software para instalar SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="install-your-report-server"></a>Instalar al servidor de informes

Instalar a un servidor de informes es sencillo. Hay solo unos pocos pasos para instalar los archivos.

> [!NOTE]
> No es necesario un servidor de motor de base de datos de SQL Server disponible en el momento de la instalación. Necesitará uno para configurar Reporting Services después de la instalación.

1. Busque la ubicación de SQLServerReportingServices.exe e inicie el programa de instalación.

2. Seleccione **instalar Reporting Services**.

    ![Instalar Reporting Services](media/install-reporting-services/report-server-install.png)

3. Elija una edición para instalar y, a continuación, seleccione **siguiente**.

    ![Elija la edición](media/install-reporting-services/report-server-install-edition.png)

    Puede elegir Evaluation o Developer edition en la lista hacia abajo.

    ![Ediciones Evaluation o developer](media/install-reporting-services/report-server-install-edition-select.png)

    De lo contrario, puede especificar una clave de producto.

4. Leer y acepte los términos de licencia y condiciones y, a continuación, seleccione **siguiente**.

5. Debe tener un motor de base de datos disponible para almacenar la base de datos del servidor de informes. Seleccione **siguiente** para instalar solo el servidor de informes.

    ![No se necesita para la instalación de la base de datos](media/install-reporting-services/report-server-install-db-engine.png)

6. Especifique la ubicación de instalación del servidor de informes. Seleccione **instalar** para continuar.

    ![Especifique la ruta de instalación](media/install-reporting-services/report-server-install-file-path.png)

    > [!NOTE]
    > La ruta predeterminada es C:\Program Files\Microsoft SQL Server Reporting Services.

7. Después de una instalación correcta, seleccione **configurar servidor de informes** para iniciar el Administrador de configuración de Reporting Services.

    ![Configurar el servidor de informes](media/install-reporting-services/report-server-install-configure.png)

## <a name="configuration-your-report-server"></a>Configuración de su servidor de informes

Después de seleccionar **configurar servidor de informes** en el programa de instalación, se le mostrará con **el Administrador de configuración del servidor de informes**. Para obtener más información, consulte [el Administrador de configuración del servidor de informes](reporting-services-configuration-manager-native-mode.md).

Necesita [crear una base de datos del servidor de informes](ssrs-report-server-create-a-report-server-database.md) para completar la configuración inicial de Reporting Services. Un servidor de base de datos de SQL Server es necesario para completar este paso.

### <a name="creating-a-database-on-a-different-server"></a>Crear una base de datos en un servidor diferente

Si va a crear la base de datos del servidor de informes en un servidor de base de datos en un equipo diferente, debe cambiar la cuenta de servicio del servidor de informes a una credencial que se reconoce en el servidor de base de datos.

De forma predeterminada, el servidor de informes utiliza la cuenta de servicio virtual. Si intenta crear una base de datos en un servidor diferente, puede recibir el siguiente error en el paso de derechos de conexión de aplicación.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Para solucionar el error, puede cambiar la cuenta de servicio a servicio de red o una cuenta de dominio. Cambiar la cuenta de servicio al servicio de red aplica derechos en el contexto de la cuenta de equipo del servidor de informes.

Para obtener más información, consulte [configurar la cuenta de servicio del servidor de informes](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## <a name="windows-service"></a>Servicio de Windows

Se crea un servicio de windows como parte de la instalación. Se muestra como **SQL Server Reporting Services**. El nombre de servicio es **SQLServerReportingServices**.

## <a name="default-url-reservations"></a>Reservas de direcciones URL predeterminadas

Las reservas de direcciones URL están compuestas de un prefijo, un nombre de host, un puerto y un directorio virtual:

|Parte|Descripción|
|----------|-----------------|
|Prefijo|El prefijo predeterminado es HTTP. Si instaló anteriormente un certificado de capa de Sockets seguros (SSL), el programa de instalación intenta crear reservas de direcciones URL que utilizan el prefijo HTTPS.|
|Nombre de host|El nombre de host predeterminado es un carácter comodín (+) seguro. Especifica que el servidor de informes acepta cualquier solicitud HTTP en el puerto designado para cualquier nombre de host que se resuelve en el equipo, incluidos los `http://<computername>/reportserver`, `http://localhost/reportserver`, o`http://<IPAddress>/reportserver.`|
|Puerto|El puerto predeterminado es 80. Si utiliza cualquier puerto distinto al puerto 80, tendrá que agregarlo explícitamente a la dirección URL al abrir el portal web en una ventana del explorador.|
|Directorio virtual|De forma predeterminada, los directorios virtuales se crean en el formato de servidor de informes para el servicio Web del servidor de informes y los informes para el portal web. Para el servicio web del servidor de informes, el nombre del directorio virtual predeterminado es **reportserver**. El portal web, el directorio virtual predeterminado es **informes**.|

Un ejemplo de cadena de dirección URL completa podría ser el siguiente:

- `http://+:80/reportserver`, proporciona acceso al servidor de informes.

- `http://+:80/reports`, proporciona acceso al portal web.

## <a name="firewall"></a>Firewall

Si el servidor de informes tiene acceso desde un equipo remoto, desea asegurarse de que ha configurado ninguna regla de firewall si hay un firewall está presente.

Deberá abrir el puerto TCP que haya configurado para la dirección URL del servicio Web y la dirección URL del Portal Web. De forma predeterminada, se configuran en el puerto TCP 80.

## <a name="additional-configuration"></a>Configuración adicional

- Para configurar la integración con el servicio Power BI, de modo que puede anclar elementos de informe a un panel de Power BI, consulte [integrar con el servicio Power BI](power-bi-report-server-integration-configuration-manager.md).

- Para configurar el correo electrónico para el procesamiento de suscripciones, consulte [configuración de correo electrónico](e-mail-settings-reporting-services-native-mode-configuration-manager.md) y [entrega en un servidor de informes de correo electrónico](../subscriptions/e-mail-delivery-in-reporting-services.md).

- Para configurar el portal web para que pueda acceder en un equipo remoto para ver y administrar informes, consulte [configurar un firewall para el acceso al servidor de informes](../report-server/configure-a-firewall-for-report-server-access.md) y [configurar un servidor de informes para la administración remota](../report-server/configure-a-report-server-for-remote-administration.md) .

## <a name="related-information"></a>Información relacionada

Para obtener información sobre cómo instalar SQL Server 2016 Reporting Services en modo nativo, vea [servidor de informes de modo nativo de instalación de Reporting Services](install-reporting-services-native-mode-report-server.md). Para obtener información sobre cómo instalar SQL Server 2016 Reporting Services en modo integrado de SharePoint, vea [instalar el primer servidor de informes en modo de SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

## <a name="next-steps"></a>Pasos siguientes

Con el servidor de informes instalado, empezar a crear informes e impleméntelas en el servidor de informes. Para obtener información sobre cómo empezar con el generador de informes, consulte [Install Report Builder](../../reporting-services/install-windows/install-report-builder.md).

Para crear informes mediante SQL Server Data Tools, [descargar SQL Server Data Tools](http://go.microsoft.com/fwlink/?LinkID=616714).

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
