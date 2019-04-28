---
title: Ver la página, los informes (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d36a9e8b5e4b46283b78f07c27834a79993faeab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62647687"
---
# <a name="view-page-reports-report-manager"></a>Ver la página, informes (Administrador de informes)
  Use la página Ver para ver un informe. La primera vez que se abre un informe en el Administrador de informes, tiene formato HTML. Los informes HTML incluyen una barra de herramientas que aparece en la parte superior del informe, de modo que pueda navegar por las páginas del informe, realizar búsquedas en el informe, o bien exportar el informe a otro formato. El diagrama siguiente muestra la barra de herramientas de informe.  
  
 ![Barra de herramientas de informe](media/htmlviewer-toolbar.gif "Barra de herramientas de informe")  
Barra de herramientas de informe  
  
 En [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], los informes se pueden configurar para ejecutarse a petición o desde una instantánea de ejecución de informes. Si un informe se ejecuta a petición, todo el procesamiento de datos y de informes se produce cada vez que abra el informe. Si ve un informe que está configurado para ejecutarse como instantánea de ejecución de informes. el procesamiento de datos se produjo cuando se creó la instantánea.  
  
## <a name="exporting-reports"></a>Exportar informes  
 No todas las características de informe está disponibles en todos los formatos de exportación. Si exporta un informe HTML a otro formato, tenga en cuenta que quizás aprecie algunas diferencias de apariencia. Asimismo, si el informe incluye características interactivas, como hipervínculos, marcadores o mapas de documento, puede que esas características no estén disponibles o no funcionen igual en el nuevo formato.  
  
## <a name="generating-data-feeds-from-report-data"></a>Generar fuentes de distribución de datos a partir de datos de informe  
 Puede generar las fuentes de los datos a partir de informes. La extensión de representación de Atom de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] genera dos documentos compatibles con Atom: un documento de servicio de Atom que enumera las fuentes de distribución de datos que proporciona el informe y las fuentes de distribución de datos que contienen los datos del informe. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] genera fuentes de distribución de datos en un formato normalizado compatible con Atom 1.0 que lo pueden leer y compartir aplicaciones que consumen fuentes de distribución de datos compatibles con Atom. Por ejemplo, el cliente de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] puede consumir fuentes de distribución de datos que se generan a partir de informes.  
  
## <a name="running-parameterized-reports"></a>Ejecutar informes parametrizados  
 Un informe con parámetros es un informe que contiene campos de entrada y un botón **Ver informe** . Para ver un informe con parámetros, es posible que deba suministrar los valores que se utilizan para ejecutar el informe.  
  
> [!NOTE]  
>  Las instantáneas de ejecución de informes y algunos formatos de exportación no están disponibles en todas las ediciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obtener más información, vea [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
