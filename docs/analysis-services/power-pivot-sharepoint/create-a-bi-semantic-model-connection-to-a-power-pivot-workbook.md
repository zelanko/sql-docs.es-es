---
title: "Crear una conexión de modelo semántico de BI a un libro PowerPivot | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2e3f97f-18a8-42b6-9030-b4f818afc3b9
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: abf47bc1e00a810eb82dfc2e34a95a60d05e84c4
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="create-a-bi-semantic-model-connection-to-a-power-pivot-workbook"></a>Crear una conexión de modelo semántico de BI a un libro PowerPivot
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Utilice la información de este tema para configurar una conexión de modelo semántico de BI que redirija a un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de la misma granja.  
  
 Después de crear una conexión de modelo semántico de BI y configurar los permisos de SharePoint, puede utilizarla como origen de datos para Excel o informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 En este tema se incluyen las secciones siguientes. Realice cada tarea en el orden indicado.  
  
 [Requisitos previos de revisión](#bkmk_prereq)  
  
 [Crear una conexión](#bkmk_create)  
  
 [Configurar permisos de SharePoint en la conexión de modelo semántico de BI](#bkmk_permissions)  
  
 [Configurar permisos de SharePoint en el libro](#bkmk_userdb)  
  
 [Pasos siguientes](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> Requisitos previos de revisión  
 Debe tener permisos de contribución o superiores para poder crear un archivo de conexión de modelo semántico de BI.  
  
 Debe tener una biblioteca que admita el tipo de contenido de la conexión de modelo semántico de BI. Para obtener más información, vea [Agregar un tipo de contenido de conexión de modelo semántico de BI a una biblioteca &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md).  
  
 Debe conocer la dirección URL de la [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] libro para el que está configurando una conexión de modelo semántico de BI (por ejemplo, `http://adventure-works/shared documents/myworkbook.xlsx`). El libro debe estar en la misma granja.  
  
 Todos los equipos y usuarios que forman parte de la secuencia de conexión deben estar en el mismo dominio o en dominios de confianza (confianza bidireccional).  
  
##  <a name="bkmk_create"></a> Crear una conexión  
  
1.  En la biblioteca que contendrá la conexión de modelo semántico de BI, haga clic en **Documentos** en la cinta de opciones de SharePoint. Haga clic en la flecha abajo en Nuevo documento y seleccione **Archivo de conexión BISM** para abrir la página Nueva conexión de modelo semántico de BI.  
  
     ![Submenú nuevo documento en una biblioteca de SharePoint](../../analysis-services/power-pivot-sharepoint/media/ssas-bismconnection-new.gif "submenú nuevo documento en una biblioteca de SharePoint")  
  
2.  Establezca la propiedad **Servidor** en la dirección URL de SharePoint del libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (por ejemplo, `http://mysharepoint/shared documents/myWorkbook.xlsx`. En una implementación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, los datos se pueden cargar en cualquier servidor de la granja. Por este motivo, las conexiones de origen de datos a datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] especifican solo la ruta de acceso al libro. El Servicio de sistema de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] determina qué servidor carga los datos.  
  
     No utilice la propiedad **base de datos** ; no se utiliza al especificar la ubicación de un libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
     El aspecto de su página deberá ser parecido al de la ilustración siguiente.  
  
     ![Página de conexión de BISM que muestra la dirección URL al libro](../../analysis-services/power-pivot-sharepoint/media/ssas-bismconnection-ppvtds.gif "página de conexión de BISM que muestra la dirección URL al libro")  
  
     Opcionalmente, si tiene permisos de SharePoint para el libro, realice un paso adicional de validación para asegurarse de que la ubicación es válida. Si no tiene permiso para obtener acceso a los datos, se le ofrecerá la opción de guardar la conexión de modelo semánticos de BI sin la respuesta de validación.  
  
##  <a name="bkmk_permissions"></a> Configurar permisos de SharePoint en la conexión de modelo semántico de BI  
 La capacidad de utilizar una conexión de modelo semántico de BI como origen de datos en un libro de Excel o un informe de Reporting Services requiere permisos de **Lectura** en el elemento de conexión de modelo semántico de BI de una biblioteca de SharePoint. El nivel de permiso de lectura incluye el permiso **Abrir elementos** , que permite descargar la información de la conexión de modelo semántico de BI en una aplicación de escritorio de Excel.  
  
 Hay varias maneras de conceder permisos de SharePoint. Las instrucciones siguientes explican cómo crear un grupo denominado **Usuarios de BISM** que tenga el nivel de permiso de **Lectura** .  
  
 Debe ser propietario del sitio para cambiar los permisos.  
  
1.  En Acciones del sitio, haga clic en **Permisos de sitio**.  
  
2.  Haga clic **Crear grupo** y asigne al nuevo grupo el nombre **Usuarios de BISM**.  
  
3.  Elija el nivel de permiso de **Lectura** y haga clic en **Crear**.  
  
4.  Seleccione **Usuarios de BISM** en usuarios y grupos.  
  
5.  Seleccione Nuevo, haga clic en **Agregar usuarios**y, a continuación, agregue cuentas de usuario o grupo.  
  
     Estos usuarios y grupos tendrán ahora permisos de Lectura en el sitio, incluidas todas las bibliotecas y las listas que hereden permisos del nivel de sitio. Si estos permisos son demasiado elevados, puede quitar selectivamente este grupo de determinadas bibliotecas, listas, o elementos.  
  
 Para quitar selectivamente permisos en el nivel de elemento, haga lo siguiente:  
  
1.  En una biblioteca, seleccione un documento. Haga clic en la flecha abajo a la derecha y después haga clic en **Administrar permisos**.  
  
2.  Un elemento hereda, de forma predeterminada, los permisos. Para cambiar los permisos de documentos individuales en esta biblioteca, haga clic en **Dejar de heredar permisos**.  
  
3.  Active la casilla junto a **Usuarios de BISM**.  
  
4.  Haga clic en **Quitar permisos de usuario**.  
  
##  <a name="bkmk_userdb"></a> Configurar permisos de SharePoint en el libro  
 Si utiliza una base de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un libro de Excel, los permisos de SharePoint del libro de Excel determinarán el acceso a los datos a través de la conexión de modelo semántico de BI. Todos los usuarios que tengan acceso al libro deben tener permisos de Lectura en el libro para poder utilizarlo como origen de datos externo.  
  
 Si creó un grupo de **usuarios de BISM** utilizando las instrucciones de la sección anterior, las cuentas de usuario y de grupo que pertenecen a los **usuarios de BISM** tendrán permisos suficientes en el libro, así como el archivo de conexión de modelo semántico de BI, suponiendo que el libro utilice permisos heredados.  
  
##  <a name="bkmk_next"></a> Pasos siguientes  
 Después de crear y proteger una conexión de modelo semántico de BI, podrá especificarla como origen de datos. Para obtener más información, vea [Usar una conexión de modelo semántico de BI en Excel o Reporting Services](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Conexión del modelo semántico de BI de PowerPivot &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Utilizar una conexión de modelo semántico de BI en Excel o Reporting Services](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md)   
 [Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-tabular-model-database.md)  
  
  
