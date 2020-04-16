---
title: Almacenamiento de las credenciales en un origen de datos de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 74380cde599c965b64c0389f51df4dc51b54bdbf
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388287"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Almacenamiento de las credenciales en un origen de datos de Reporting Services
  Es posible configurar credenciales almacenadas que un servidor de informes de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] use para obtener acceso a los datos externos de un informe. Las credenciales almacenadas se utilizan si un informe se ejecuta de forma desatendida, por ejemplo, una suscripción [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que publica un informe como correo electrónico. El servidor de informes recupera y usa las credenciales cuando se programa o desencadena el procesamiento de informes. En este tema se explica cómo configurar credenciales almacenadas para los servidores de informes en modo Nativo y en modo de SharePoint.

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] | Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]|

 **En este tema:**

-   [Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)](#bkmk_stored_credentials_data_source_native)

-   [Configurar credenciales almacenadas para un origen de datos específico de informe (modo de SharePoint)](#bkmk_stored_credentials_data_source_sharepoint)

-   [Configurar credenciales almacenadas para un origen de datos compartido (modo Nativo)](#bkmk_stored_credentials_shared_data_source_native)

-   [Configurar credenciales almacenadas para un origen de datos compartido (modo SharePoint)](#bkmk_stored_credentials_shared_data_source_sharepoint)

##  <a name="security-policy-requirements-for-stored-credentials"></a><a name="bkmk_top"></a> Requisitos de directiva de seguridad para credenciales almacenadas
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") Es necesario que la cuenta que usa para las credenciales almacenadas se configure para una de las siguientes directivas de seguridad en el servidor de informes. Se recomienda seleccionar la directiva con el nivel mínimo de permisos necesario para el entorno.

1.  **Permitir iniciar sesión localmente**. Para obtener más información, vea [Permitir el inicio de sesión local](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).

2.  **Iniciar sesión como proceso por lotes**. Para obtener más información, vea [Iniciar sesión como proceso por lotes](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).

3.  Para obtener información general sobre directivas, vea [Modificar la configuración de seguridad en un objeto de directiva de grupo](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).

##  <a name="configure-stored-credentials-for-a-report-specific-data-source-native-mode"></a><a name="bkmk_stored_credentials_data_source_native"></a>Configurar credenciales almacenadas para un origen de datos específico del informe (modo nativo)

1.  En el modo Nativo del Administrador de informes, vaya a la carpeta que contiene el informe. Haga clic en el menú contextual del menú contextual del elemento en el administrador de ![informes para los elementos ssrs](../media/ssrs-report-manager-item-context-menu.png "menú contextual en el administrador de informes para elementos de ssrs").

2.  Haga clic en **Administrar** y luego en **Orígenes de datos**.

3.  Seleccione **Un origen de datos personalizado**.

4.  En la lista **Tipo de origen de datos** , seleccione la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.

5.  En **Cadena de conexión**, especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. En el ejemplo siguiente se muestra una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] cadena de conexión utilizada para conectarse a la base de datos:

    ```
    data source=<servername>;initial catalog=AdventureWorks2012
    ```

6.  En **Conectar utilizando**, seleccione **Credenciales almacenadas de forma segura en el servidor de informes**.

7.  Escriba un nombre de usuario y una contraseña.

    -   Si la cuenta es una cuenta de usuario \<de \\ dominio\>de Windows, estibérala en este formato: dominio><cuenta y, a continuación, seleccione Usar como credenciales de **Windows al conectarse al origen** de datos.

    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.

8.  Haga clic en **Aplicar**.

     ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)

##  <a name="configure-stored-credentials-for-a-report-specific-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_data_source_sharepoint"></a>Configurar credenciales almacenadas para un origen de datos específico del informe (modo SharePoint)

1.  Vaya a la biblioteca de documentos que contiene el informe y haga clic en el menú Abrir ![menú contextual de la biblioteca de documentos para elementos de ssrs](../media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs").

2.  Haga clic en el segundo menú Abrir ![menú contextual de la biblioteca de documentos para elementos de ssrs](../media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs") y, luego, haga clic en **Administrar orígenes de datos**.

3.  Haga clic en el nombre del origen de datos **personalizado** que quiere configurar con credenciales almacenadas.

4.  En la lista **Tipo de origen de datos** , seleccione la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.

5.  En **Cadena de conexión**, especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. En el ejemplo siguiente se muestra una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] cadena de conexión utilizada para conectarse a la base de datos:

    ```
    data source=<servername>;initial catalog=AdventureWorks2012
    ```

6.  En **Credenciales**, seleccione **Credenciales almacenadas**.

7.  Escriba un nombre de **usuario** y **una contraseña.**

    -   Si la cuenta es una cuenta de usuario \<de \\ dominio\>de Windows, estibérala en este formato: dominio><cuenta y, a continuación, seleccione Usar como credenciales de **Windows al conectarse al origen** de datos.

    -   Si el nombre de usuario y la contraseña son credenciales de base de datos, no seleccione **Utilizar como credenciales de Windows**. Si el servidor de bases de datos admite la suplantación o delegación, puede seleccionar Establecer contexto de ejecución en **esta cuenta.**

8.  Haga clic en **Ok** (Aceptar).

     ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)

##  <a name="configure-stored-credentials-for-a-shared-data-source-native-mode"></a><a name="bkmk_stored_credentials_shared_data_source_native"></a>Configurar credenciales almacenadas para un origen de datos compartido (modo nativo)

1.  En el modo Nativo del Administrador de informes, vaya al elemento del origen de datos compartido. ![Icono de origen de datos compartido](../media/hlp-16datasource.png "Icono de origen de datos compartido")

2.  Haga clic en el menú contextual del menú contextual en el administrador de ![informes para los elementos ssrs](../media/ssrs-report-manager-item-context-menu.png "menú contextual en el administrador de informes para elementos de ssrs") y, a continuación, haga clic en **Administrar**.

3.  En la lista Tipo de **origen** de datos, especifique la extensión de procesamiento de datos que se usa para procesar datos del origen de datos.

4.  En **Cadena de conexión**, especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomienda que no especifique credenciales en la cadena de conexión.

     En el ejemplo siguiente se muestra una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] cadena de conexión utilizada para conectarse a la base de datos local:

    ```
    data source=<localservername>; initial catalog=AdventureWorks2012
    ```

5.  Escriba un nombre de usuario y una contraseña.

    -   Si la cuenta es una cuenta de usuario \<de \\ dominio\>de Windows, estibérala en este formato: dominio><cuenta y, a continuación, seleccione Usar como credenciales de **Windows al conectarse al origen** de datos.

    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.

6.  Haga clic en **Aplicar**.

     ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)

##  <a name="configure-stored-credentials-for-a-shared-data-source-sharepoint-mode"></a><a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Configurar credenciales almacenadas para un origen de datos compartido (modo de SharePoint)

1.  En la biblioteca de documentos, vaya al elemento de origen de datos compartido.![Icono Origen de datos compartido](../media/hlp-16datasource.png "Icono de origen de datos compartido")

2.  Haga clic en el menú contextual ![menú contextual de la biblioteca de documentos para elementos de ssrs](../media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs") y, luego, haga clic en el segundo menú contextul ![menú contextual de la biblioteca de documentos para elementos de ssrs](../media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs").

3.  Haga clic en **Editar definición de origen de datos**.

4.  En la lista Tipo de **origen** de datos, especifique la extensión de procesamiento de datos que se usa para procesar datos del origen de datos.

5.  En **Cadena de conexión**, especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomienda que no especifique credenciales en la cadena de conexión.

     En el ejemplo siguiente se muestra una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] cadena de conexión utilizada para conectarse a la base de datos local:

    ```
    data source=<localservername>; initial catalog=AdventureWorks2012
    ```

6.  Escriba un nombre de usuario y una contraseña.

    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela con este formato: \<dominio>\\<cuenta\> y seleccione **Usar como credenciales de Windows**.

    -   Si el nombre de usuario y la contraseña son credenciales de base de datos, no seleccione **Utilizar como credenciales de Windows**. Si el servidor de base de datos admite suplantación o delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.

7.  Haga clic en **Aceptar**.

     ![Icono de flecha usado con el vínculo Volver al principio](../../2014-toc/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)

## <a name="see-also"></a>Consulte también
 [Especificar la información de credenciales y conexión para orígenes](../../integration-services/connection-manager/data-sources.md) de datos de informe Configurar propiedades del origen de datos para un informe &#40;el Administrador de [informes&#41;](configure-data-source-properties-for-a-report-report-manager.md) [crear, eliminar o modificar un origen](../create-delete-or-modify-a-shared-data-source-report-manager.md) de datos compartido &#40;página Propiedades del Administrador de informes&#41;&#40;Administrador de [informes&#41;](../data-sources-properties-page-report-manager.md) Nueva página del origen de datos &#40;administrador de [informes&#41;](../new-data-source-page-report-manager.md)


