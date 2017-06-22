---
title: "Recopilación de datos de Control de ReportViewer 2016 | Documentos de Microsoft"
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
caps.latest.revision: 2
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4e8b0226c27380bd2089acf8d2d6c8d7b27c7c5b
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integrar Reporting Services con los controles ReportViewer: recopilación de datos
De forma predeterminada, el ReportViewer Control recopila información anónima de uso en orden para que Microsoft pueda entender mejor cómo los clientes realizan uso del control. Mediante la creación de una mejor comprensión de cómo va a implementar y usar el Control de Visor de los clientes, que puede concentrarse desarrollo futuro sobre las mejoras que brindan mayor valor a los clientes.

Para ver una explicación de las prácticas de recopilación y uso de datos de usuario de las versiones de Microsoft SQL Server 2016 y de cualquier otro producto y servicio, consulte esta [declaración de privacidad de Microsoft](https://www.microsoft.com/EN-US/privacystatement/SQLServer/Default.aspx).

## <a name="opting-out-of-telemetry"></a>No participar en de telemetría

Telemetría puede deshabilitarse mediante programación a través de la "EnableTelemetry". Esto puede hacerse mediante la edición de la página .aspx que hospeda el control

```
\<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
\</rsweb:ReportViewer>
```

O bien, pragmática antes de que el control se representa tal como se muestra en llamadas de Page_Load de la página de hospedaje.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Vea también

[Usar el Control WebForms ReportViewer](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integrar Reporting Services con los controles ReportViewer](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 




