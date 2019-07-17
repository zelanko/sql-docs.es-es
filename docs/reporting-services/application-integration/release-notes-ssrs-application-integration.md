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
ms.openlocfilehash: 1528358c8aff5d6e99869f0f4f8c1676ee2d5e75
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67730908"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Notas de la versión para los controles de Visor de informes para formularios Web Forms y formularios Windows Forms de SSRS

Estas son las notas de los controles de Visor de informes de formularios Web Forms y formularios Windows Forms, relacionados con [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Para las notas de la versión de SSRS, consulte [notas de la versión para SQL Server Reporting Services (SSRS) 2017 y versiones posteriores](../release-notes-reporting-services.md).

## <a name="15013580"></a>150.1358.0
| Descripción del cambio | Detalles |
| :----------------- | :------ |
| Correcciones de errores | Revertir un cambio que quita los ensamblados Microsoft.ReportViewer.Design de las referencias del proyecto. |
|           | Como parte de otros cambios, los dos ensamblados se cambiaron desde la versión 15.0 a 15.3. Se ha revertido. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Descripción del cambio | Detalles |
| :----------------- | :------ |
| Correcciones de errores  | Vista previa de impresión adecuada para el monitor de alta concentración de PPP |
|            | Cuadro de diálogo de impresión mostraría fuera del espacio visible |
|            | Dio como resultado un gran número de parámetros en las barras de desplazamiento de parámetro y las listas desplegables no funciona correctamente |
|            | Se corrigió un problema con los parámetros de tiempo es Null y la fecha |
|            | JQuery actualizado a la versión 3.3.1 |
|            | Se ha corregido la superposición con las celdas de tablix de representación en HTML |
|            | Quita el tiempo de diseño que se hace referencia un proyecto para eliminar ensamblados de VS erróneos que se agrega a los proyectos |
|            | Accesibilidad corrección de la barra de herramientas para narrar solo para elementos activos |
| &nbsp; | &nbsp; |

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
