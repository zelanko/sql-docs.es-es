---
title: Notificaciones del servicio de Token de Windows (c2WTS) y Reporting Services | Documentos de Microsoft
ms.custom: The Claims to Windows Token Service (C2WTS) is used by SharePoint and needs to be configured for Kerberos constrained delegation to work with SQL Server Reporting Services properly.
ms.date: 09/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a9397f427cac18d0c8bfc663f6bd477b0440b8a3
ms.openlocfilehash: 8a478bba3cde66967594d5ef02f867de5b33edd7
ms.contentlocale: es-es
ms.lasthandoff: 09/15/2017

---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Notificaciones del servicio de token de Windows (C2WTS) y Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

Notificaciones del servicio de Token de Windows (C2WTS) es necesaria si desea ver informes en modo nativo en el [elemento web de Visor de informes de SQL Server Reporting Services](../report-server-sharepoint/deploy-report-viewer-web-part.md).

C2WTS también es necesario con el modo de SharePoint de SQL Server Reporting Services si desea utilizar la autenticación de Windows para orígenes de datos que se encuentran fuera de la granja de servidores de SharePoint. C2WTS es necesario aunque los orígenes de datos estén en el mismo equipo que el servicio compartido. Sin embargo, en este escenario no es necesaria la delegación restringida.

> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

## <a name="report-viewer-web-part-configuration"></a>Configuración de parte de web de Visor de informes

El elemento web Visor de informes se puede utilizar para incrustar informes de modo nativo de SQL Server Reporting Services en el sitio de SharePoint. Este elemento web está disponible para SharePoint 2013 y SharePoint 2016. SharePoint 2013 y SharePoint 2016 hacen que el uso de autenticación de notificaciones. SQL Server Reporting Services (modo nativo) utiliza la autenticación de Windows de forma predeterminada. Como resultado, C2WTS debe configurarse correctamente para que los informes que se muestre correctamente.

## <a name="sharepoint-mode-integaration"></a>Integaration de modo de SharePoint

**Esta sección solo se aplica a SQL Server 2016 Reporting Services y versiones anteriores.**

Notificaciones del servicio de Token de Windows (C2WTS) se requiere con el modo de SharePoint de SQL Server Reporting Services si desea utilizar la autenticación de Windows para orígenes de datos que se encuentran fuera de la granja de servidores de SharePoint. Esto es cierto incluso si el usuario tiene acceso a los orígenes de datos con la autenticación de Windows porque la comunicación entre el front-end web (WFE) y el servicio compartido de Reporting Services siempre será autenticación de notificaciones.

## <a name="steps-needed-to-configure-c2wts"></a>Pasos necesarios para configurar c2WTS

Los tokens creados por C2WTS funcionarán solo con delegación restringida (limitaciones a servicios concretos) y la opción de configuración "Usar cualquier protocolo de autenticación". Como se indicaba anteriormente, si los orígenes de datos están en el mismo equipo que el servicio compartido, la delegación restringida no es necesaria.

Si en su entorno se usa la delegación limitada de Kerberos, el servicio SharePoint Server y los orígenes de datos externos deben residir en el mismo dominio de Windows. Cualquier servicio que use Notificaciones del servicio de token de Windows (c2WTS) debe emplear la delegación **restringida** de Kerberos para permitir que c2WTS use la transición del protocolo Kerberos para traducir las notificaciones en credenciales de Windows. Estos requisitos son verdaderos para todos los servicios compartidos de SharePoint. Para obtener más información, vea [Planear la autenticación Kerberos en SharePoint 2013](http://technet.microsoft.com/library/ee806870.aspx).  

1. Configurar la cuenta de servicio de C2WTS. Agregue la cuenta de servicio al grupo de administradores local en cada servidor que va a usar C2WTS.

    Para el **elemento web Visor de informes de**, se trata de los servidores Web Front-End (WFE). Para **el modo integrado de SharePoint**, se trata de los servidores de aplicaciones donde se está ejecutando el servicio de Reporting Services.

2. Configurar la delegación para la cuenta de servicio de C2WTS.

    La cuenta necesita una delegación restringida con transición de protocolo así como permisos para delegar a los servicios que se requiere para comunicarse con (es decir, SQL Server Database Engine, SQL Server Analysis Services). Para configurar la delegación puede utilizar el complemento de usuarios de Active Directory y el equipo y deberá ser un administrador de dominio.

    > [!IMPORTANT]
    > Cualquier configuración de se configura para la cuenta de servicio de C2WTS, en la pestaña de delegación, debe coincidir con la cuenta de servicio principal que se va a usar. Para el **elemento web Visor de informes de**, se trata de la cuenta de servicio para la aplicación web de SharePoint. Para **el modo integrado de SharePoint**, se trata de la cuenta de servicio de Reporting Services.
    >
    > Por ejemplo, si permite que la cuenta de servicio de C2WTS delegar a un servicio de SQL, debe hacer lo mismo en la cuenta de servicio de Reporting Services para el modo integrado de SharePoint.

    * Haga clic con el botón secundario en cada cuenta de servicio y abra el cuadro de diálogo de propiedades. En el cuadro de diálogo, haga clic en la pestaña **Delegación** .

        La pestaña delegación solo está visible si el objeto tiene un nombre de entidad de seguridad de servicio (SPN) asignados a él. C2WTS no requiere un SPN en la cuenta de C2WTS, sin embargo, sin un SPN, el **delegación** ficha no serán visible. Una manera alternativa de configurar la delegación restringida es utilizar una herramienta como **ADSIEdit**.

    * Las opciones de configuración clave en la pestaña de delegación son las siguientes:

        * Seleccione **confiar en este usuario para la delegación sólo a servicios especificados**
        * Seleccione **usar cualquier protocolo de autenticación**

    * Seleccione **Agregar** para agregar un servicio en el que delegar.

    * Seleccione **usuarios o equipos...** * y escriba la cuenta que hospeda el servicio. Por ejemplo, si un servidor SQL Server se ejecuta con una cuenta llamada *sqlservice*, escriba `sqlservice`. 

    * Seleccione la lista de servicios. Esto mostrará los SPN disponibles en esa cuenta. Si el servicio no está indicado en la cuenta, es posible que falte o que esté en otra cuenta. Puede usar la utilidad SetSPN para ajustar los SPN.

    * Seleccione Aceptar para salir de los cuadros de diálogo.

3. Configurar C2WTS *AllowedCallers*.

    C2WTS requiere que las identidades de 'llamadores' explícitamente enumerados en el archivo de configuración, **C2WTShost.exe.config**. C2WTS no acepta solicitudes de todos los usuarios autenticados en el sistema a menos que esté configurado para ello. En este caso el "llamador" es el grupo de Windows WSS_WPG. El archivo C2WTShost.exe.confi se guarda en la siguiente ubicación:

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

4. Inicie las notificaciones al servicio de Token de Windows mediante Administración Central de SharePoint en el **administrar servicios en el servidor** página. El servicio se debe iniciar en el servidor que realizará la acción. Por ejemplo, si tiene un servidor que es WFE y otro servidor que es un servidor de aplicaciones con el servicio compartido de SQL Server Reporting Services en ejecución, que sólo deben iniciar C2WTS en el servidor de aplicaciones. C2WTS solo es necesario en un servidor de WFE si está ejecutando el elemento web Visor de informes.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).
