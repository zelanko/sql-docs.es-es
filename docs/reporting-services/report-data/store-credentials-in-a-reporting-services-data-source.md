---
title: Almacenar credenciales en un origen de datos de Reporting Services | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 09/23/2015
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- credentials [Reporting Services]
- security [Analysis Services], data sources
- stored credentials [Reporting Services]
- data sources [Reporting Services], stored credentials
ms.assetid: dc700922-97fa-4b30-9547-05bbbec4f09c
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6ca8d81025d48af07b5e2ce9336a8e031ea4fb1a
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="store-credentials-in-a-reporting-services-data-source"></a>Almacenar credenciales en un origen de datos de Reporting Services
  Es posible configurar credenciales almacenadas que un servidor de informes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] use para obtener acceso a los datos externos de un informe. Las credenciales almacenadas se utilizan si un informe se ejecuta de forma desatendida, por ejemplo, una suscripción [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que publica un informe como correo electrónico. El servidor de informes recupera y usa las credenciales cuando se programa o desencadena el procesamiento de informes. En este tema se explica cómo configurar credenciales almacenadas para los servidores de informes en modo Nativo y en modo de SharePoint.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
  
-   [Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)](#bkmk_stored_credentials_data_source_native)  
  
-   [Configurar credenciales almacenadas para un origen de datos específico de informe (modo de SharePoint)](#bkmk_stored_credentials_data_source_sharepoint)  
  
-   [Configurar credenciales almacenadas para un origen de datos compartido (modo Nativo)](#bkmk_stored_credentials_shared_data_source_native)  
  
-   [Configurar credenciales almacenadas para un origen de datos compartido (modo de SharePoint)](#bkmk_stored_credentials_shared_data_source_sharepoint)  
  
##  <a name="bkmk_top"></a> Requisitos de directiva de seguridad para credenciales almacenadas  
 ![as_powerpivot_refresh_sss_set_key](../../analysis-services/power-pivot-sharepoint/media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key") es necesario que la cuenta que use para las credenciales almacenadas, está configurado para una de las siguientes directivas de seguridad en el servidor de informes. Se recomienda seleccionar la directiva con el nivel mínimo de permisos necesario para el entorno.  
  
1.  **Permitir el inicio de sesión local**. Para obtener más información, vea [Permitir el inicio de sesión local](http://technet.microsoft.com/library/cc756809\(v=WS.10\).aspx).  
  
2.  **Iniciar sesión como proceso por lotes**. Para obtener más información, vea [Iniciar sesión como proceso por lotes](http://technet.microsoft.com/library/cc755659\(v=ws.10\).aspx).  
  
3.  Para obtener información general sobre directivas, vea [Modificar la configuración de seguridad en un objeto de directiva de grupo](http://technet.microsoft.com/library/cc736516\(v=ws.10\).aspx).  
  
##  <a name="bkmk_stored_credentials_data_source_native"></a> Configurar credenciales almacenadas para un origen de datos específico de informe (modo Nativo)  
  
1.  En el modo Nativo del Administrador de informes, vaya a la carpeta que contiene el informe. Haga clic en el menú contextual del elemento ![menú contextual en el Administrador de informes para elementos de ssrs](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "menú contextual en el Administrador de informes para elementos de ssrs").  
  
2.  Haga clic en **Administrar** y luego en **Orígenes de datos**.  
  
3.  Seleccione **Un origen de datos personalizado**.  
  
4.  En la lista **Tipo de origen de datos** , seleccione la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
5.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  En **Conectar utilizando**, seleccione **Credenciales almacenadas de forma segura en el servidor de informes**.  
  
7.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela en este formato: \<dominio >\\< cuenta\>y, a continuación, seleccione **utilizar como credenciales de Windows al conectarse al origen de datos.**  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.  
  
8.  Haga clic en **Aplicar**.  
  
     ![Icono de flecha usado con Back vínculo al principio](../../analysis-services/instances/media/uparrow16x16.gif "icono de flecha usado con Back vínculo al principio") [requisitos de la directiva de seguridad para las credenciales almacenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_data_source_sharepoint"></a> Configurar credenciales almacenadas para un origen de datos específico de informe (modo de SharePoint)  
  
1.  Vaya a la biblioteca de documentos que contiene el informe y, a continuación, haga clic en el menú Abrir ![menú de contexto de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú de contexto de la biblioteca de documentos para elementos de ssrs").  
  
2.  Haga clic en el segundo menú abierto ![menú de contexto de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú de contexto de la biblioteca de documentos para elementos de ssrs") y, a continuación, haga clic en **administrar orígenes de datos**.  
  
3.  Haga clic en el nombre del origen de datos **personalizado** que quiere configurar con credenciales almacenadas.  
  
4.  En la lista **Tipo de origen de datos** , seleccione la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
5.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<servername>;initial catalog=AdventureWorks2012  
    ```  
  
6.  En **Credenciales**, seleccione **Credenciales almacenadas**.  
  
7.  Escriba un **nombre de usuario** y una **contraseña**.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela en este formato: \<dominio >\\< cuenta\>y, a continuación, seleccione **utilizar como credenciales de Windows al conectarse al origen de datos.**  
  
    -   Si el nombre de usuario y la contraseña son credenciales de base de datos, no seleccione **Utilizar como credenciales de Windows**. Si el servidor de base de datos admite la suplantación o la delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
8.  Haga clic en **Aceptar**.  
  
     ![Icono de flecha usado con Back vínculo al principio](../../analysis-services/instances/media/uparrow16x16.gif "icono de flecha usado con Back vínculo al principio") [requisitos de la directiva de seguridad para las credenciales almacenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_native"></a> Configurar credenciales almacenadas para un origen de datos compartido (modo Nativo)  
  
1.  En el modo Nativo del Administrador de informes, vaya al elemento del origen de datos compartido. ![Icono de origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "Icono de origen de datos compartido")  
  
2.  Haga clic en el menú contextual ![menú contextual en el Administrador de informes para elementos de ssrs](../../reporting-services/report-data/media/ssrs-report-manager-item-context-menu.png "menú contextual en el Administrador de informes para elementos de ssrs") y, a continuación, haga clic en **administrar**.  
  
3.  En la lista **Tipo de origen de datos** , especifique la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
4.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer la conexión con la base de datos local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
5.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela en este formato: \<dominio >\\< cuenta\>y, a continuación, seleccione **utilizar como credenciales de Windows al conectarse al origen de datos.**  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de bases de datos admite la suplantación o la delegación, puede seleccionar **Suplantar al usuario autenticado después de realizar una conexión al origen de datos**.  
  
6.  Haga clic en **Aplicar**.  
  
     ![Icono de flecha usado con Back vínculo al principio](../../analysis-services/instances/media/uparrow16x16.gif "icono de flecha usado con Back vínculo al principio") [requisitos de la directiva de seguridad para las credenciales almacenadas](#bkmk_top)  
  
##  <a name="bkmk_stored_credentials_shared_data_source_sharepoint"></a> Configurar credenciales almacenadas para un origen de datos compartido (modo de SharePoint)  
  
1.  En la biblioteca de documentos, busque el elemento de origen de datos compartido. ![Icono de origen de datos compartido](../../reporting-services/report-data/media/hlp-16datasource.png "icono de origen de datos compartido")  
  
2.  Haga clic en el menú contextual ![menú de contexto de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú de contexto de la biblioteca de documentos para elementos de ssrs") y, a continuación, haga clic en el segundo menú contextual ![menú de contexto de la biblioteca de documentos para elementos de ssrs](../../reporting-services/report-data/media/ssrs-sharepoint-item-context-menu.png "menú de contexto de la biblioteca de documentos para elementos de ssrs").  
  
3.  Haga clic en **Editar definición de origen de datos**.  
  
4.  En la lista **Tipo de origen de datos** , especifique la extensión de procesamiento de datos que se usa para procesar los datos del origen de datos.  
  
5.  En **Cadena de conexión**, especifique la cadena de conexión que usa el servidor de informes para conectarse al origen de datos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] recomienda que no especifique credenciales en la cadena de conexión.  
  
     En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer la conexión con la base de datos local [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
6.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela en este formato: \<dominio >\\< cuenta\>y, a continuación, seleccione **utilizar como credenciales de Windows.**  
  
    -   Si el nombre de usuario y la contraseña son credenciales de base de datos, no seleccione **Utilizar como credenciales de Windows**. Si el servidor de base de datos admite suplantación o delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
7.  Haga clic en **Aceptar**.  
  
     ![Icono de flecha usado con Back vínculo al principio](../../analysis-services/instances/media/uparrow16x16.gif "icono de flecha usado con Back vínculo al principio") [requisitos de la directiva de seguridad para las credenciales almacenadas](#bkmk_top)  
  
## <a name="see-also"></a>Vea también  
 [Especificar credenciales y la información de conexión para orígenes de datos de informe](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Configurar propiedades de origen de datos para un informe &#40; El Administrador de informes &#41;](../../reporting-services/report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Crear, eliminar o modificar un origen de datos compartido &#40; El Administrador de informes &#41;](http://msdn.microsoft.com/library/cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2)   
 [Página de propiedades de orígenes de datos &#40; El Administrador de informes &#41;](http://msdn.microsoft.com/library/f37edda0-19e6-489e-b544-8751fa6b6cfb)   
 [Nueva página de origen de datos &#40; El Administrador de informes &#41;](http://msdn.microsoft.com/library/35563d4c-a3d5-4f95-bf46-605da9dfcbb8)  
  
  

