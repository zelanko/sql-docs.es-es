---
title: Cargar documentos en informes de biblioteca de SharePoint modo de SharePoint Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- SharePoint integration [Reporting Services], content management
- uploading reports [Reporting Services]
ms.assetid: 93bd1b19-061b-409f-8dc2-ec416b2f4b39
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 51cf021c47749367bba6fcc08081dfeed688298f
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>Cargar documentos en una biblioteca de SharePoint (Reporting Services en el modo integrado de SharePoint)
  Puede cargar definiciones de informe y modelos de informe en una biblioteca de SharePoint. Al cargar un elemento del servidor de informes, debe seleccionar una biblioteca o una carpeta dentro de una biblioteca. No se puede cargar un elemento del servidor de informes en una lista o en una página.  
  
 No puede cargar un archivo de origen de datos (.rds). No obstante, puede publicar archivos .rds de una herramienta de diseño, como el Diseñador de informes, en una biblioteca de SharePoint. Durante la publicación, se crea un nuevo archivo .rsds a partir del archivo .rds original de la solución. También puede crear un nuevo archivo .rsds en una biblioteca de SharePoint y, a continuación, establecer las propiedades de conexión de origen de datos en los informes y modelos cargados para usar la nueva conexión.  
  
> [!NOTE]  
>  El servidor de informes debe configurarse para el modo de SharePoint y la instancia del producto de SharePoint debe tener el complemento de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , que proporciona archivos de programa para almacenar y obtener acceso a los elementos del servidor de informes desde un sitio de SharePoint.  
  
 Para cargar un documento en una biblioteca, debe contar con el permiso "Agregar elementos" en el nivel de sitio. Si está utilizando la configuración de seguridad predeterminada, este permiso se concederá a los miembros del grupo **Propietarios** que tengan un nivel de permiso Control total y a los miembros del grupo **Miembros** que tengan un nivel de permiso Colaborar.  
  
### <a name="to-add-a-report-definition-or-report-model-to-a-library"></a>Para agregar una definición de informe o modelo de informe a una biblioteca  
  
1.  Abra la biblioteca o una carpeta que se encuentre dentro de una biblioteca. Si la biblioteca no está abierta todavía, haga clic en su nombre en Inicio rápido. Si no aparece el nombre de la biblioteca, haga clic en **Ver todo el contenido del sitio**y, a continuación, haga clic en el nombre de la biblioteca.  
  
2.  En el menú **Cargar** , haga clic en **Cargar documento**.  
  
3.  Para cargar un único informe o archivo de modelo de informe, seleccione un archivo de definición de informe (.rdl) o un archivo de modelo de informe (.smdl) y, después, haga clic en **Aceptar**.  
  
     Si la definición de informe usa un archivo de origen de datos compartido (.rsds) para almacenar la información de conexión en un origen de datos externo, podrá cargar los archivos .rdl y .rsds al mismo tiempo. Para ello, haga clic en **Cargar varios documentos**, especifique ambos archivos y haga clic en **Aceptar**.  
  
 Si ha cargado un informe que incluye referencias a orígenes de datos compartidos, modelos de informe o subinformes, las referencias se anularán en el informe cuando se carguen los archivos. Para obtener más información sobre cómo restablecer las referencias, vea [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Al cargar un informe, el informe se ejecuta a petición al abrirlo, y se recuperan datos actualizados del origen de datos. Puede configurar el informe para recuperar datos en una programación o usar datos almacenados en caché. Para obtener más información, vea [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 Un informe puede incluir parámetros, de modo que los usuarios puedan filtrar los datos. Puede configurar los parámetros para usar valores específicos o cambiar el modo en que se presentan al usuario. Para obtener más información, vea [Establecer parámetros en un informe publicado &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Vea también  
 [Publicar un informe en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Publicar un origen de datos compartido en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Conceder permisos sobre elementos de servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  
  
  
