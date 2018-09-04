---
title: Notificaciones del servicio de token de Windows (C2WTS) y Reporting Services | Microsoft Docs
ms.date: 09/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.suite: pro-bi
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a4092aa6f801d1f3f521cffc088e8b345495267b
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/30/2018
ms.locfileid: "43275612"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Notificaciones del servicio de token de Windows (C2WTS) y Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Las Notificaciones del servicio de token de Windows (C2WTS) de SharePoint son necesarias si quiere ver informes en modo nativo en el [elemento web de Visor de informes de SQL Server Reporting Services](../report-server-sharepoint/deploy-report-viewer-web-part.md).

C2WTS también es necesario con el modo de SharePoint de SQL Server Reporting Services si quiere usar la autenticación de Windows para los orígenes de datos que están fuera de la granja de SharePoint. C2WTS es necesario aunque los orígenes de datos estén en el mismo equipo que el servicio compartido. Sin embargo, en este escenario no es necesaria la delegación restringida.

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

## <a name="report-viewer-web-part-configuration"></a>Configuración del elemento web Visor de informes

El elemento web Visor de informes se puede usar para insertar informes de SQL Server Reporting Services (modo nativo) en el sitio de SharePoint. Este elemento web está disponible para SharePoint 2013 y SharePoint 2016. Tanto en SharePoint 2013 como en SharePoint 2016 se hace uso de la autenticación de notificaciones. SQL Server Reporting Services (modo nativo) usa la autenticación de Windows de forma predeterminada. Como resultado, se debe configurar C2WTS de forma adecuada para que los informes se muestren correctamente.

## <a name="sharepoint-mode-integaration"></a>Integración del modo de SharePoint

**Esta sección solo se aplica a SQL Server 2016 Reporting Services y versiones anteriores.**

Se necesita Notificaciones del servicio de token de Windows (C2WTS) de SharePoint con el modo de SharePoint de SQL Server Reporting Services si quiere usar la autenticación de Windows para los orígenes de datos que están fuera de la granja de SharePoint. Esto es cierto incluso si el usuario obtiene acceso a los orígenes de datos con la autenticación de Windows porque la comunicación entre el servicio front-end web (WFE) y el servicio compartido de Reporting Services se realizará siempre con la autenticación de notificaciones.

## <a name="steps-needed-to-configure-c2wts"></a>Pasos necesarios para configurar c2WTS

Los tokens creados por C2WTS funcionarán solo con delegación restringida (limitaciones a servicios concretos) y la opción de configuración "Usar cualquier protocolo de autenticación". Como se indicaba anteriormente, si los orígenes de datos están en el mismo equipo que el servicio compartido, la delegación restringida no es necesaria.

Si en su entorno se usa la delegación limitada de Kerberos, el servicio SharePoint Server y los orígenes de datos externos deben residir en el mismo dominio de Windows. Cualquier servicio que use Notificaciones del servicio de token de Windows (c2WTS) debe emplear la delegación **restringida** de Kerberos para permitir que c2WTS use la transición del protocolo Kerberos para traducir las notificaciones en credenciales de Windows. Estos requisitos son verdaderos para todos los servicios compartidos de SharePoint. Para obtener más información, vea [Planear la autenticación Kerberos en SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  

1. Configure la cuenta de servicio C2WTS. Agregue la cuenta de servicio al grupo de administradores local en cada servidor en el que se va a usar C2WTS.

    Para el **elemento web Visor de informes**, serán los servidores front-end web (WFE). Para **el modo integrado de SharePoint**, serán los servidores de aplicaciones donde se ejecuta el servicio de Reporting Services.

2. Configure la delegación para la cuenta de servicio de C2WTS.

    La cuenta necesita una delegación restringida con transición de protocolo así como permisos para delegar a los servicios con los que requiere comunicación (es decir, Motor de base de datos de SQL Server, SQL Server Analysis Services). Para configurar la delegación se puede usar el complemento Usuarios y equipos de Active Directory y es necesario ser administrador de dominio.

    > [!IMPORTANT]
    > Las opciones que configure para la cuenta de servicio de C2WTS, en la pestaña de delegación, deben coincidir con las de la cuenta de servicio principal que se usa. Para el **elemento web Visor de informes**, se trata de la cuenta de servicio para la aplicación web de SharePoint. Para **el modo integrado de SharePoint**, se trata de la cuenta de servicio de Reporting Services.
    >
    > Por ejemplo, si permite que la cuenta de servicio de C2WTS delegue en un servicio de SQL, debe hacer lo mismo en la cuenta de servicio de Reporting Services para el modo integrado de SharePoint.

    * Haga clic con el botón secundario en cada cuenta de servicio y abra el cuadro de diálogo de propiedades. En el cuadro de diálogo, haga clic en la pestaña **Delegación** .

        La pestaña de delegación solo está visible si el objeto tiene asignado un nombre de entidad de seguridad de servicio (SPN). C2WTS no requiere un SPN en la cuenta de C2WTS, pero sin un SPN, la pestaña **Delegación** no estará visible. Una manera alternativa de configurar la delegación restringida es utilizar una herramienta como **ADSIEdit**.

    * Las opciones de configuración clave en la pestaña de delegación son las siguientes:

        * Seleccionar **Confiar en este usuario para la delegación solo a los servicios especificados**
        * Seleccionar **Usar cualquier protocolo de autenticación**

    * Seleccione **Agregar** para agregar un servicio en el que delegar.

    * Seleccione **Usuarios o equipos...*** y escriba la cuenta que hospeda el servicio. Por ejemplo, si un servidor SQL Server se ejecuta en una cuenta denominada *sqlservice*, escriba `sqlservice`. 

    * Seleccione la lista de servicios. Esto mostrará los SPN disponibles en esa cuenta. Si el servicio no está indicado en la cuenta, es posible que falte o que esté en otra cuenta. Puede usar la utilidad SetSPN para ajustar los SPN.

    * Seleccione Aceptar para salir de los cuadros de diálogo.

3. Configure *AllowedCallers* de C2WTS.

    C2WTS requiere que las identidades de los "autores de la llamada" estén enumeradas explícitamente en el archivo de configuración, **C2WTShost.exe.config**. C2WTS no acepta solicitudes de todos los usuarios autenticados en el sistema a menos que esté configurado para ello. En este caso el "autor de la llamada" es el grupo de Windows WSS_WPG. El archivo C2WTShost.exe.config se guarda en la ubicación siguiente:

    Si cambia la cuenta de servicio en la Administración central de SharePoint para el servicio C2WTS, agregará esa cuenta al grupo WSS_WPG.

    **\Archivos de programa\Windows Identity Foundation\v3.5\c2WTShost.exe.config**

    A continuación se muestra un ejemplo del archivo de configuración:

    ```
    <configuration>
      <windowsTokenService>
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->
        <allowedCallers>
          <clear/>
          <add value="WSS_WPG" />
        </allowedCallers>
      </windowsTokenService>
    </configuration>
    ```

4. Inicie las Notificaciones del servicio de token de Windows a través de la Administración central de SharePoint en la página **Administrar servicios en el servidor**. El servicio se debe iniciar en el servidor que realizará la acción. Por ejemplo, si tiene un servidor que es un servidor web front-end (WFE) y otro servidor que es un servidor de aplicaciones que tiene la ejecución del servicio compartido de SQL Server Reporting Services, solo tiene que iniciar C2WTS en el servidor de aplicaciones. C2WTS solo es necesario en un servidor WFE si se está ejecutando el elemento web Visor de informes.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
