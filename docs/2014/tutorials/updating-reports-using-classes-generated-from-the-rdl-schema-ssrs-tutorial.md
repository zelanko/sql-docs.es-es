---
title: Actualizar informes con clases generadas a partir del esquema RDL (Tutorial de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
caps.latest.revision: 26
author: craigg-msft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 96d125a3d69b564c94b64d23f825778c55068991
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37297565"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>Actualizar informes con clases generadas a partir del esquema RDL (Tutorial de SSRS)
  En este tutorial se muestra cómo usar la herramienta de definición de esquemas XML (Xsd.exe) para generar clases que permiten serializar y deserializar archivos de definición de informe (.rdl y .rdlc) con el [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer> clase.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En el transcurso de este tutorial, realizará las actividades siguientes:  
  
-   Cree una aplicación con el [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] plantilla de proyecto de aplicación de consola.  
  
-   Generar clases a partir del esquema de lenguaje RDL (Report Definition Language) mediante el **xsd** herramienta.  
  
-   Conectarse a un servidor de informes y recuperar una definición de informe.  
  
-   Escribir un código para actualizar el archivo de definición de informe.  
  
-   Guardar la definición de informe actualizada en el servidor de informes.  
  
-   Ejecutar la aplicación del esquema RDL (VB/C#).  
  
> [!NOTE]  
>  Los ejemplos de código proporcionados en este tutorial pueden provocar errores en los informes que no tengan una descripción. El error se debe a que la propiedad de descripción no existe en los informes en los que no se ha especificado una descripción.  
  
## <a name="requirements"></a>Requisitos  
 Para poder completar el tutorial en su totalidad, debe disponer de lo siguiente:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)].  
  
-   Permisos suficientes para tener acceso al servicio web del servidor de informes y publicar informes en este servicio en el equipo en que se encuentre el servidor de informes.  
  
-   La base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] instalada en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Un informe instalado en el servidor de informes. En este tutorial se utiliza el informe de muestra Company Sales 2012. Para obtener más información acerca de los informes de ejemplo, vea [SQL Server Reporting Services Product Samples](http://go.microsoft.com/fwlink/?LinkId=177889).  
  
> [!NOTE]  
>  Los ejemplos no se instalan automáticamente durante la ejecución del programa de instalación, pero puede instalarlos en cualquier momento. Para obtener información acerca de los ejemplos, vea [SQL Server Product Samples](http://go.microsoft.com/fwlink/?LinkId=182887).  
  
 **Tiempo estimado para completar el tutorial:** 30 minutos  
  
## <a name="tasks"></a>Tareas  
 [Lección 1: Crear el proyecto de Visual Studio de la aplicación Esquema RDL](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [Lección 2: Generar clases a partir del esquema RDL con la herramienta xsd](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [Lección 3: Cargar una definición de informe desde el servidor de informes](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [Lección 4: Actualizar la definición del informe mediante programación](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [Lección 5: Publicar la definición de informe en el servidor de informes](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [Lección 6: Ejecutar la aplicación del esquema RDL &#40;VB-C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>Vea también  
 [Report Definition Language &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
