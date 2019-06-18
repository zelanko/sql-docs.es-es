---
title: Notas de la versión de los controles del Visor de informes de SSRS
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maghan
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6d4da6d5574288fa66ea18a9c63b1488a6abcca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63226001"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Notas de la versión para los controles de Visor de informes para formularios Web Forms y formularios Windows Forms de SSRS

Estas son las notas de los controles de Visor de informes de formularios Web Forms y formularios Windows Forms, relacionados con [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Para las notas de la versión de SSRS, consulte [notas de la versión para SQL Server Reporting Services (SSRS) 2017 y versiones posteriores](../release-notes-reporting-services.md).

## <a name="15900148"></a>15.900.148

| Descripción del cambio | Detalles |
| :----------------- | :------ |
| Corrija un error que impide que los informes sin parámetros se carguen a través de **Server.LoadReportDefinition**. | &nbsp; |
| El control del Visor de informes WebForms. | Compatibilidad con la inserción en las páginas de derecha a izquierda (páginas que cambian el flujo de texto mediante la propiedad css *direction: rtl;* ).<br/><br/>Compatibilidad con la personalización de texto del cuadro de diálogo de impresión a través de la interfaz de localización *IReportViewerMessages5*.<br/><br/>Compatibilidad de accesibilidad mejorada.<br/><br/>&bull; &nbsp; &nbsp; [Paquete de NuGet para el control de Visor de informes de WebForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| El control del Visor de informes WinForms. | Corrección para la impresión cuando se ejecuta una aplicación en modo con valores altos de PPP.<br/><br/>&bull; &nbsp; &nbsp; [Paquete de NuGet para el control de Visor de informes de Windows Forms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Pasos siguientes

[Introducción](integrating-reporting-services-using-reportviewer-controls-get-started.md) a los controles del Visor de informes.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
