---
title: Actualizar informes con clases generadas a partir del esquema RDL (tutorial de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 313a5268b754089d4ca8964328d53cb23ec6edd1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62746119"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>Actualizar informes con clases generadas a partir del esquema RDL (Tutorial de SSRS)
  En este tutorial se muestra cómo utilizar la herramienta de definición de esquemas XML (XSD. exe) para generar clases que le permitan serializar y deserializar archivos de definición de informe (. RDL [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer> y. rdlc) con la clase.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En el transcurso de este tutorial, realizará las actividades siguientes:  
  
-   Cree una aplicación con la [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] plantilla de proyecto aplicación de consola.  
  
-   Generar clases a partir del esquema del lenguaje RDL (Report Definition Language) mediante la herramienta **xsd** .  
  
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
  
-   Un informe instalado en el servidor de informes. En este tutorial se utiliza el informe de muestra Company Sales 2012. Para obtener más información sobre los informes de ejemplo, vea [SQL Server Reporting Services ejemplos de productos](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
> [!NOTE]  
>  Los ejemplos no se instalan automáticamente durante la ejecución del programa de instalación, pero puede instalarlos en cualquier momento. Para obtener información acerca de los ejemplos, vea [SQL Server ejemplos de productos](https://go.microsoft.com/fwlink/?LinkId=182887).  
  
 **Tiempo estimado para completar el tutorial:** 30 minutos  
  
## <a name="tasks"></a>Tareas  
 [Lección 1: Crear el proyecto de Visual Studio de la aplicación Esquema RDL](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [Lección 2: Generar clases a partir del esquema RDL con la herramienta xsd](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [Lección 3: Cargar una definición de informe desde el servidor de informes](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [Lección 4: Actualizar la definición del informe mediante programación](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [Lección 5: Publicar la definición de informe en el servidor de informes](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [Lección 6: ejecutar la aplicación de esquema RDL &#40;VB-C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>Consulte también  
 [Lenguaje RDL (Report Definition Language) &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
