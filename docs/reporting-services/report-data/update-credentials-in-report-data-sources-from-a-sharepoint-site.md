---
title: "Actualizar credenciales en orígenes de datos de informe desde un sitio de SharePoint | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 85652be59a369ff3b571f8858a744962b5b3f619
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>Actualizar credenciales en orígenes de datos de informe desde un sitio de SharePoint
  En este tema se describe cómo actualizar los orígenes de datos incrustados en informes y los orígenes de datos compartidos en una biblioteca de documentos de SharePoint.  
  
 Muchos de sus informes pueden incluir orígenes de datos o utilizar orígenes de datos compartidos configurados para usar la autenticación de Windows. En algunas circunstancias, como cuando crea alertas de datos para informes guardados en una biblioteca de documentos de SharePoint, tendrá que actualizar las credenciales del origen de datos a las credenciales almacenadas o no requerir ninguna credencial.  
  
 Para utilizar credenciales almacenadas en informes, puede decidir crear y usar un nuevo inicio de sesión de SQL Server. Para obtener más información, vea [Crear un inicio de sesión](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>Para actualizar un origen de datos incrustado de modo que use credenciales almacenadas  
  
1.  Vaya a la biblioteca de documentos de SharePoint donde guardó el informe.  
  
2.  Haga clic en el icono para expandir el menú desplegable del informe y, después, haga clic en **Administrar orígenes de datos**.  
  
     Se abre la página Administrar orígenes de datos.  
  
3.  En la columna **Nombre** , haga clic en el origen de datos.  
  
4.  Para **Tipo de conexión** , compruebe que la opción **Origen de datos personalizado** esté seleccionada.  
  
     Esta opción indica que el origen de datos está incrustado en el informe.  
  
5.  Deje las opciones **Tipo de origen de datos** y **Cadena de conexión** tal como están, a menos que desee que el informe se conecte a un tipo diferente de origen de datos, a un servidor diferente o a un almacén de datos.  
  
6.  Para **Credenciales**, seleccione **Credenciales almacenadas**. Esta opción solo funciona si el origen de datos no acepta credenciales o si se pasan credenciales de otra manera.  
  
     En algunas circunstancias se puede usar también la opción **No se necesitan credenciales** .  
  
     En algunos tipos de orígenes de datos, se debe configurar una cuenta de ejecución desatendida en el servidor de informes. Para más información, vea el tema del tipo de origen de datos correspondiente en [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) y [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
7.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela en este formato: \<dominio >\\< cuenta\>y, a continuación, seleccione **utilizar como credenciales de Windows al conectarse al origen de datos**.  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de base de datos admite la suplantación o la delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
8.  Para comprobar que el origen de datos se puede conectar usando las credenciales actualizadas, haga clic en **Probar conexión**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>Para actualizar un origen de datos compartido de modo que use credenciales almacenadas  
  
1.  Vaya a la biblioteca de documentos de SharePoint donde guardó el origen de datos compartido.  
  
2.  Haga clic en el icono para expandir el menú desplegable del origen de datos compartido y, después, haga clic en **Editar definición de origen de datos**.  
  
     Se abre la página Origen de datos.  
  
3.  Deje las opciones **Tipo de origen de datos** y **Cadena de conexión** tal como están, a menos que desee que el origen de datos compartido se conecte a un tipo diferente de origen de datos, a un servidor diferente o a un almacén de datos.  
  
4.  Para **Credenciales**, seleccione **Credenciales almacenadas**.  
  
     En algunas circunstancias se puede usar también la opción **No se necesitan credenciales** . Esta opción solo funciona si el origen de datos no acepta credenciales o si se pasan credenciales de otra manera.  
  
     En algunos tipos de orígenes de datos, se debe configurar una cuenta de ejecución desatendida en el servidor de informes. Para más información, vea el tema del tipo de origen de datos correspondiente en [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) y [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
5.  Escriba un nombre de usuario y una contraseña.  
  
    -   Si la cuenta es una cuenta de usuario de dominio de Windows, especifíquela en este formato: \<dominio >\\< cuenta\>y, a continuación, seleccione **utilizar como credenciales de Windows al conectarse al origen de datos.**  
  
    -   Si el nombre de usuario y la contraseña son credenciales de la base de datos, no seleccione **Utilizar como credenciales de Windows para la conexión al origen de datos**. Si el servidor de base de datos admite la suplantación o la delegación, puede seleccionar **Establecer contexto de ejecución en esta cuenta**.  
  
6.  Para comprobar que el origen de datos se puede conectar usando las credenciales actualizadas, haga clic en **Probar conexión**.  
  
7.  Compruebe que la opción Habilitar este origen de datos está seleccionada.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Cargar documentos en una biblioteca de SharePoint &#40; Reporting Services en modo de SharePoint &#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  
