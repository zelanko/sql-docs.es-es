---
title: "Recopilación de datos del control ReportViewer 2016 | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 112e0240-351d-46a9-98c7-2be09f26ac60
caps.latest.revision: "2"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b2f5f4743b838598aeb5f74271fa063af9bb60f3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integración de Reporting Services con los controles ReportViewer: recopilación de datos
De forma predeterminada, el control ReportViewer recopila información anónima de uso para que Microsoft pueda entender mejor cómo lo usan los clientes. Analizando el modo en que implementan y usan el control ReportViewer, el desarrollo futuro se puede centrar en mejoras que ofrezcan mayor valor a los clientes.

Para ver una explicación de las prácticas de recopilación y uso de datos de usuario de las versiones de Microsoft SQL Server 2016 y de cualquier otro producto y servicio, consulte esta [declaración de privacidad de Microsoft](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx).

## <a name="opting-out-of-telemetry"></a>Deshabilitar la telemetría

La telemetría se puede deshabilitar mediante programación con la opción "EnableTelemetry". Para ello, debe editar la página .aspx que hospeda el control.

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

También se puede hacer de forma pragmática antes de que se represente el control, como en la llamada Page_Load de la página de hospedaje.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Vea también

[Usar el control ReportViewer de WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrar Reporting Services con los controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



