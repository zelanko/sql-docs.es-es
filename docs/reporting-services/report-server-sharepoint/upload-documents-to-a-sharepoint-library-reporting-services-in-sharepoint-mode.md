---
title: Cargar documentos en una biblioteca de SharePoint (Reporting Services en el modo de SharePoint) | Microsoft Docs
description: En el modo de SharePoint de SQL Server Reporting Services, puede cargar definiciones y modelos de informe en una biblioteca de SharePoint.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: a7a9e0aaf57d3084e6be239cb8fedcdd3d2e9066
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2020
ms.locfileid: "83767367"
---
# <a name="upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode"></a>Cargar documentos en una biblioteca de SharePoint (Reporting Services en el modo de SharePoint)

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Puede cargar definiciones de informe y modelos de informe en una biblioteca de SharePoint. Al cargar un elemento del servidor de informes, debe seleccionar una biblioteca o una carpeta dentro de una biblioteca. No se puede cargar un elemento del servidor de informes en una lista o en una página.  

> [!NOTE]
> La integración de Reporting Services con SharePoint ya no está disponible a partir de SQL Server 2016.

 No puede cargar un archivo de origen de datos (.rds). No obstante, puede publicar archivos .rds de una herramienta de diseño, como el Diseñador de informes, en una biblioteca de SharePoint. Durante la publicación, se crea un nuevo archivo .rsds a partir del archivo .rds original de la solución. También puede crear un nuevo archivo .rsds en una biblioteca de SharePoint y, a continuación, establecer las propiedades de conexión de origen de datos en los informes y modelos cargados para usar la nueva conexión.  
  
> [!NOTE]  
>  El servidor de informes debe configurarse para el modo de SharePoint y la instancia del producto de SharePoint debe tener el complemento de Reporting Services, que proporciona archivos de programa para almacenar y obtener acceso a los elementos del servidor de informes desde un sitio de SharePoint.  
  
 Para cargar un documento en una biblioteca, debe contar con el permiso "Agregar elementos" en el nivel de sitio. Si está utilizando la configuración de seguridad predeterminada, este permiso se concederá a los miembros del grupo **Propietarios** que tengan un nivel de permiso Control total y a los miembros del grupo **Miembros** que tengan un nivel de permiso Colaborar.  
  
## <a name="add-a-report-definition-or-report-model-to-a-library"></a>Agregar una definición de informe o un modelo de informe a una biblioteca
  
1.  Abra la biblioteca o una carpeta que se encuentre dentro de una biblioteca. Si la biblioteca no está abierta todavía, haga clic en su nombre en Inicio rápido. Si no aparece el nombre de la biblioteca, haga clic en **Ver todo el contenido del sitio**y, a continuación, haga clic en el nombre de la biblioteca.  
  
2.  En el menú **Cargar** , haga clic en **Cargar documento**.  
  
3.  Para cargar un único informe o archivo de modelo de informe, seleccione un archivo de definición de informe (.rdl) o un archivo de modelo de informe (.smdl) y, después, haga clic en **Aceptar**.  
  
     Si la definición de informe usa un archivo de origen de datos compartido (.rsds) para almacenar la información de conexión en un origen de datos externo, podrá cargar los archivos .rdl y .rsds al mismo tiempo. Para ello, haga clic en **Cargar varios documentos**, especifique ambos archivos y haga clic en **Aceptar**.  
  
 Si ha cargado un informe que incluye referencias a orígenes de datos compartidos, modelos de informe o subinformes, las referencias se anularán en el informe cuando se carguen los archivos. Para más información sobre cómo restablecer las referencias, vea [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
 Al cargar un informe, el informe se ejecuta a petición al abrirlo, y se recuperan datos actualizados del origen de datos. Puede configurar el informe para recuperar datos en una programación o usar datos almacenados en caché. Para más información, vea [Establecer opciones de procesamiento &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-server-sharepoint/set-processing-options-reporting-services-in-sharepoint-integrated-mode.md).  
  
 Un informe puede incluir parámetros, de modo que los usuarios puedan filtrar los datos. Puede configurar los parámetros para usar valores específicos o cambiar el modo en que se presentan al usuario. Para más información, vea [Establecer parámetros en un informe publicado &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/report-design/set-parameters-on-a-published-report-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Consulte también

 [Publicar un informe en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-report-to-a-sharepoint-library.md)   
 [Publicación de un origen de datos compartido en una biblioteca de SharePoint](../../reporting-services/reports/publish-a-shared-data-source-to-a-sharepoint-library.md)   
 [Concesión de permisos sobre elementos del servidor de informes en un sitio de SharePoint](../../reporting-services/security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
