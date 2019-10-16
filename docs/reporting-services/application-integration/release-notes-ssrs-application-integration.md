---
title: Notas de la versión de los controles del Visor de informes de SSRS
ms.date: 09/20/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
ms.reviewer: maggies
author: RhysSchmidtke
ms.author: rhys
ms.openlocfilehash: d6c7130e45e535ad1849bed5713313bf6f89020f
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923814"
---
# <a name="release-notes-for-the-report-viewer-controls-for-webforms-and-winforms-of-ssrs"></a>Notas de la versión de los controles del visor de informes para WebForms y WinForms de SSRS

Estas son las notas de la versión de los controles de visor de informes de WebForms y WinForms, relacionadas con [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS).

Para obtener las notas de la versión de SSRS, consulte las [notas de la versión de SQL Server Reporting Services (SSRs) 2017 y versiones posteriores](../release-notes-reporting-services.md).

## <a name="15013580"></a>150.1358.0
| Cambiar Descripción | Detalles |
| :----------------- | :------ |
| Correcciones de errores | Ha revertido un cambio que ha quitado los ensamblados Microsoft. ReportViewer. Design de las referencias del proyecto. |
|           | Como parte de otros cambios, se cambiaron dos ensamblados de la versión 15,0 a 15,3. Esto se ha revertido. |
| &nbsp; | &nbsp; |

## <a name="15013570"></a>150.1357.0
| Cambiar Descripción | Detalles |
| :----------------- | :------ |
| Correcciones de errores  | Vista previa de impresión adecuada para monitor de alta resolución de PPP |
|            | El cuadro de diálogo Imprimir se mostraría fuera del espacio visible |
|            | Un gran número de parámetros provocó que las barras de desplazamiento de parámetros y las listas desplegables no funcionaran correctamente |
|            | Se corrigió un problema con los parámetros de fecha y hora nulos |
|            | JQuery actualizado a la versión 3.3.1 |
|            | Se corrigió la superposición con celdas de Tablix en representación en HTML |
|            | Se han quitado las referencias de proyecto en tiempo de diseño para eliminar los ensamblados de VS erróneos que se agregan a los proyectos |
|            | Corrección de accesibilidad de la barra de herramientas para narrar solo los elementos activos |
| &nbsp; | &nbsp; |

## <a name="15900148"></a>15.900.148

| Cambiar Descripción | Detalles |
| :----------------- | :------ |
| Corrija un error que impide que los informes sin parámetros se carguen a través de **Server.LoadReportDefinition**. | &nbsp; |
| El control del Visor de informes WebForms. | Compatibilidad con la inserción en las páginas de derecha a izquierda (páginas que cambian el flujo de texto mediante la propiedad css *direction: rtl;* ).<br/><br/>Compatibilidad con la personalización de texto del cuadro de diálogo de impresión a través de la interfaz de localización *IReportViewerMessages5*.<br/><br/>Compatibilidad de accesibilidad mejorada.<br/><br/>paquete NuGet &bull; &nbsp; &nbsp; [para el control de visor de informes de WebForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Webforms/150.900.148) |
| El control del Visor de informes WinForms. | Corrección para la impresión cuando se ejecuta una aplicación en modo con valores altos de PPP.<br/><br/>paquete NuGet &bull; &nbsp; @no__t 2 [para el visor de informes control de WinForms](https://www.nuget.org/packages/Microsoft.ReportingServices.ReportViewerControl.Winforms/150.900.148) |
| &nbsp; | &nbsp; |

## <a name="next-steps"></a>Pasos siguientes

[Introducción](integrating-reporting-services-using-reportviewer-controls-get-started.md) a los controles del Visor de informes.

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
