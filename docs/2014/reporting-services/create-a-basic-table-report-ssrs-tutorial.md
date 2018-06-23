---
title: Crear un informe de tabla básico (Tutorial de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
caps.latest.revision: 61
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 4f8b3f60d82a94fa7289054d0028ab539abade64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113985"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>Crear un informe de tabla básico (Tutorial de SSRS)
  Este tutorial está diseñado para ayudarle a crear un informe de tabla básico basado en la [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] mediante el Diseñador de informes de la base de datos. También puede crear informes con el Generador de informes o con el Asistente para informes. En este tutorial, creará un proyecto de informes, configurará la información de conexión, definirá una consulta, agregará una región de datos de tabla, agrupará y calculará los totales de varios campos, y obtendrá una vista previa del informe.  
  
> [!NOTE]  
>  Para completar este tutorial, [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] debe ejecutarse en modo nativo. Si [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se ejecuta en el modo integrado de SharePoint, los pasos en que se usan las direcciones URL del servidor de informes no funcionan. Para obtener más información acerca de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] modos, consulte [Reporting Services Report Server](reporting-services-report-server.md).  
  
## <a name="requirements"></a>Requisitos  
 Para usar este tutorial, debe tener el software siguiente instalado en el sistema:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] motor de base de datos.  
  
-   Las base de datos [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].  Para obtener más información, consulte [Adventure Works para SQL Server 2012 (Adventure Works para SQL Server 2012)](http://go.microsoft.com/fwlink/?LinkId=245471) (http://go.microsoft.com/fwlink/?LinkId=245471).. Para obtener más información sobre la compatibilidad con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bases de datos de ejemplo y el código de ejemplo para [!INCLUDE[ssExpress](../includes/ssexpress-md.md)], consulte [Databases and Samples Overview](http://go.microsoft.com/fwlink/?LinkId=110391) en el sitio CodePlex Web.  
  
-   [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNote64Samp](../includes/ssnote64samp-md.md)]  
  
 También debe tener permisos de solo lectura para recuperar datos de la [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
## <a name="tasks"></a>Tareas  
 [Lección 1: Crear un proyecto de servidor de informes &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)  
  
 [Lección 2: Especificar información de conexión &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)  
  
 [Lección 3: Definir un conjunto de datos para el informe de tabla &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)  
  
 [Lección 4: Agregar una tabla al informe &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)  
  
 [Lección 5: Aplicar formato a un informe &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)  
  
 [Lección 6: Agregar grupos y totales &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)  
  
> [!NOTE]  
>  Para consultar los tutoriales, se recomienda que agregue **siguiente** y **anterior** botones a la barra de herramientas del Visor de documentos. Para obtener más información, vea:  
  
## <a name="see-also"></a>Vea también  
 [Tutoriales de Reporting Services &#40;SSRS&#41;](reporting-services-tutorials-ssrs.md)  
  
  