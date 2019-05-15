---
title: Recopilación de datos del control ReportViewer 2016
uthor: markingmyname
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
ms.custom: ''
ms.date: 09/18/2018
ms.openlocfilehash: f1d24c2de0b6398b4effb2dcaa6129a7b252d130
ms.sourcegitcommit: e4794943ea6d2580174d42275185e58166984f8c
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65504132"
---
# <a name="integrating-reporting-services-using-reportviewer-controls---data-collection"></a>Integración de Reporting Services con los controles ReportViewer: recopilación de datos

El control recopila datos de uso anónimos para comprender mejor cómo los clientes usan el producto. Los datos de uso permiten que el desarrollo futuro se centre en las mejoras que sean más relevantes para los clientes.

En la [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=868444) encontrará una explicación de las prácticas de recopilación y uso de datos de Microsoft SQL Server y el Visor de informes.

## <a name="opting-out-of-data-collection"></a>Exclusión de la recopilación de datos

Se puede deshabilitar la recopilación de datos de uso a través de la propiedad ```EnableTelemetry```.

```
<rsweb:ReportViewer ID="ReportViewer1" runat="server" EnableTelemetry="false">
</rsweb:ReportViewer>
```

O mediante pragmática antes de representar el control.
    
```
protected void Page_Load(object sender, EventArgs e)
{
    ReportViewer1.EnableTelemetry = false;
}
```
## <a name="see-also"></a>Vea también

[Usar el control ReportViewer de WebForms](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)  
[Integración de Reporting Services con los controles del Visor de informes](../../reporting-services/application-integration/integrating-reporting-services-using-reportviewer-controls.md) 



