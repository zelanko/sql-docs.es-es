---
title: Recopilación de datos del control ReportViewer
description: El control recopila datos de uso anónimos para comprender mejor cómo los clientes usan el producto. Los datos de uso permiten que el desarrollo futuro se centre en las mejoras que sean más relevantes para los clientes.
author: maggiesMSFT
ms.author: maggies
ms.custom: ''
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.date: 09/18/2018
ms.openlocfilehash: d7b70445fc4d8a29d8ebcdf7ecbffe4b54133f0e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "74796894"
---
# <a name="integrate-reporting-services-using-reportviewer-controls---data-collection"></a>Integración de Reporting Services con los controles ReportViewer: recopilación de datos

El control recopila datos de uso anónimos para comprender mejor cómo los clientes usan el producto. Los datos de uso permiten que el desarrollo futuro se centre en las mejoras que sean más relevantes para los clientes.

En la [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=868444) encontrará una explicación de las prácticas de recopilación y uso de datos de Microsoft SQL Server y el Visor de informes.

## <a name="opting-out-of-data-collection"></a>Exclusión de la recopilación de datos

Se puede deshabilitar la recopilación de datos de uso a través de la propiedad ```EnableTelemetry```.

```xml
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

O mediante pragmática antes de representar el control.
    
```csharp
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Consulte también

[Usar el control ReportViewer de WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integración de Reporting Services con los controles del Visor de informes](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



