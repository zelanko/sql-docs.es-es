---
title: "Crear un informe m&#243;vil en pesta&#241;as con obtenci&#243;n de detalles | Informes m&#243;viles de Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Crear un informe m&#243;vil en pesta&#241;as con obtenci&#243;n de detalles | Informes m&#243;viles de Reporting Services
Sepa cómo crear un informe móvil de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] que se vea y funcione como un informe en pestañas con obtención de detalles y parámetros.

En este informe, por ejemplo, los medidores en la parte superior actúan como pestañas. Cuando haga clic en el medidor Transporte, los datos del resto del gráfico se filtran según los datos de transporte.

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

En segundo plano, realmente esto es un conjunto de cinco informes independientes, cada uno con un parámetro diferente que filtra el informe para que coincida con el medidor seleccionado en la parte superior del informe. 

Para este ejemplo, cree cinco informes primero y, después, para cada uno de los cinco informes, convierta los otros cuatro medidores en informes detallados de los otros cuatro informes. 

Aquí se muestra un esquema de alto nivel de los pasos.

1. Cree un informe denominado Ventas, con cinco medidores:
     - Sales
     - Transporte
     - Combustible
     - Almacenamiento
     - Gastos varios
2. Realice cuatro copias del informe denominado: 
     - Transporte
     - Combustible
     - Almacenamiento
     - Gastos varios
3.  En el informe Ventas, establezca cada uno de los cuatro medidores (que no sea el medidor Ventas) como informes detallados en sus informes respectivos.

4. En el mismo informe Ventas, establezca la propiedad Accent del medidor Ventas para contrastar con el resto del informe y que destaque.

5.  Ahora, en el informe Transporte, establezca el medidor Ventas como un informe detallado del informe Ventas, y los otros tres medidores como informes detallados de sus informes respectivos.

6. De nuevo, todavía en el informe Transporte, establezca la propiedad Accent del medidor Transporte para contrastar con el resto del informe.

5. Repita lo mismo para los informes Combustible, Almacenamiento y Gastos varios. 







  
