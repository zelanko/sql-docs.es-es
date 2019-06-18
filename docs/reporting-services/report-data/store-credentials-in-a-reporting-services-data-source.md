---
title: Almacenamiento de las credenciales en un origen de datos de Reporting Services | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 05/24/2018
ms.openlocfilehash: f9f8671fa07d54ac2e682f8ed5224308dcb77ddf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65575008"
---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Almacenamiento de las credenciales en un origen de datos de Reporting Services

::: moniker range="<=sql-server-2016||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]

::: moniker-end

Es posible configurar credenciales almacenadas que un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] use para obtener acceso a los datos externos de un informe. Las credenciales almacenadas se utilizan si un informe se ejecuta de forma desatendida, por ejemplo, una suscripción [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que publica un informe como correo electrónico. El servidor de informes recupera y usa las credenciales cuando se programa o desencadena el procesamiento de informes. En este tema se explica cómo configurar credenciales almacenadas para los servidores de informes en modo Nativo y en modo de SharePoint.  
  
##  <a name="bkmk_top"></a> Requisitos de directiva de seguridad para credenciales almacenadas  
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") Es necesario que la cuenta que usa para las credenciales almacenadas se configure para una de las siguientes directivas de seguridad en el servidor de informes. Se recomienda seleccionar la directiva con el nivel mínimo de permisos necesario para el entorno.  
  
1.  **Permitir el inicio de sesión local**. Para obtener más información, vea [Permitir el inicio de sesión local](https://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Iniciar sesión como proceso por lotes**. Para obtener más información, vea [Iniciar sesión como proceso por lotes](https://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Para obtener información general sobre directivas, vea [Modificar la configuración de seguridad en un objeto de directiva de grupo](https://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)  
  
1.  En el portal web, vaya a la carpeta que contiene el informe. Haga clic en el botón de puntos suspensivos (...) en la esquina superior derecha del icono de informe.  
  
2.  Haga clic en **Administrar** y luego en **Orígenes de datos**.  
  
3.  Seleccione **Un origen de datos personalizado**.  
  
4.  En la lista **Tipo de origen de datos** , seleccione la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
5.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  En **Conectar utilizando**, seleccione **Credenciales almacenadas de forma segura en el servidor de informes**.  
  
7.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquelo con este formato: \<dominio>\\<cuenta\> y seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.  
  
8.  Haga clic en **Aplicar**.  
  
     ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> Configurar credenciales almacenadas para un origen de datos específico de informe (modo de SharePoint)  
  
1.  Vaya a la biblioteca de documentos que contiene el informe y haga clic en el menú Abrir ![menú contextual de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs").  
  
2.  Haga clic en el segundo menú Abrir ![menú contextual de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs") y, luego, haga clic en **Administrar orígenes de datos**.  
  
3.  Haga clic en el nombre del origen de datos **personalizado** que quiere configurar con credenciales almacenadas.  
  
4.  En la lista **Tipo de origen de datos** , seleccione la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
5.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  En **Credenciales**, seleccione **Credenciales almacenadas**.  
  
7.  Escriba un **nombre de usuario** y una **contraseña**.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquelo con este formato: \<dominio>\\<cuenta\> y seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de base de datos, no seleccione **Utilizar como credenciales de Windows**. Si el servidor de base de datos admite la suplantación o la delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
8.  Haga clic en **Aceptar**.  
  
     ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> Configurar credenciales almacenadas para un origen de datos compartido (modo Nativo)  
  
1.  En el portal web, vaya al elemento del origen de datos compartido. 
  
2.  Haga clic en el botón de puntos suspensivos (...) en la esquina superior derecha del icono de informe > **Administrar**. 
  
3.  En la lista **Tipo**, especifique la extensión de procesamiento de datos que se usa para procesar datos desde el origen de datos.  
  
4.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer la conexión con la base de datos local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquelo con este formato: \<dominio>\\<cuenta\> y seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.  
  
6.  Haga clic en **Aplicar**.  
  
     ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Configurar credenciales almacenadas para un origen de datos compartido (modo de SharePoint)  
  
1.  En la biblioteca de documentos, vaya al elemento de origen de datos compartido.![Icono Origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "Icono Origen de datos compartido")  
  
2.  Haga clic en el menú contextual ![menú contextual de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs") y, luego, haga clic en el segundo menú contextual ![menú contextual de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú contextual de la biblioteca de documentos para elementos de ssrs").  
  
3.  Haga clic en **Editar definición de origen de datos**.  
  
4.  En la lista **Tipo de origen de datos** , especifique la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
5.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer la conexión con la base de datos local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela con este formato: \<dominio>\\<cuenta\> y seleccione **Usar como credenciales de Windows**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de base de datos, no seleccione **Utilizar como credenciales de Windows**. Si el servidor de base de datos admite suplantación o delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
7.  Haga clic en **Aceptar**.  
  
     ![Icono de flecha usado con el vínculo Volver al principio](../../analysis-services/instances/media/uparrow16x16.gif "Icono de flecha usado con el vínculo Volver al principio") [Requisitos de directiva de seguridad para credenciales almacenadas](#bkmk_top)  
  
## <a name="see-also"></a>Consulte también  
 [Especificación de información de credenciales y conexión para los orígenes de datos de informes](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
  
