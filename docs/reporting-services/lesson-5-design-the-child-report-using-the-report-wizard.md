---
title: 'Lección 5: Diseñar el informe secundario usando el Asistente para informes | Microsoft Docs'
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: da9f07cf60a2ec42e23416b52cbfebab78802247
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "62512649"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lección 5: Diseñar el informe secundario usando el Asistente para informes
Después de crear una conexión de datos y una tabla de datos para el informe secundario, el paso siguiente consiste en diseñar dicho informe usando el Asistente para informes del Diseñador de informes. Para más información sobre el Diseñador de informes, vea [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Para diseñar el informe secundario usando el Asistente para informes  
  
1.  Asegúrese de que el sitio web de nivel superior está seleccionado en el **Explorador de soluciones**.  
  
2.  Haga clic con el botón derecho en el sitio web y seleccione **Agregar nuevo elemento**.  
  
3.  En el cuadro de diálogo **Agregar nuevo elemento** , haga clic en **Asistente para informes**, escriba un nombre para el archivo de informe y, después, seleccione **Agregar**.  
  
    Así se inicia el Asistente para informes.  
  
4.  En la página **Propiedades del conjunto de datos** , en el cuadro **Origen de datos** , seleccione **DataSet2**.  
  
    El cuadro **Conjuntos de datos disponibles** se actualiza automáticamente con el elemento DataTable que ha creado.  
  
5.  Seleccione **Next** (Siguiente).  
  
6.  En la página **Organizar campos** , haga lo siguiente:  
  
    1.  Arrastre **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**y **StockedQty** desde **Campos disponibles** hasta el cuadro **Valores** .  
  
    2.  Seleccione la flecha situada junto a **Sum(ProductID)** , **Sum(PurchaseOrderID)** , **Sum(PurchaseOrderDetailID)** , **Sum(OrderQty)** , **Sum(ReceivedQty)** , **Sum(RejectedQty)** y **Sum(StockedQty)** y desactive la selección de **Suma** .  
  
7.  Seleccione **Siguiente** dos veces y, después, haga clic en **Finalizar** para cerrar el **Asistente para informes**.  
  
    Ahora ha creado el archivo .rdlc. El archivo se abre en el Diseñador de informes. El Tablix que se diseñó se muestra en la superficie de diseño.  
  
8.  Con el archivo .rdlc abierto, agregue un parámetro haciendo lo siguiente:  
  
    1.  Haga clic con el botón derecho en **Parámetros** , en el panel **Datos de informe** , y, después, seleccione **Agregar parámetros**.  
  
    2.  Escriba **productid** en el cuadro **Nombre** .  
  
    3.  Confirme que **Entero** está seleccionado en el cuadro de lista **Tipo de datos** .  
  
    4.  Haga clic en **OK**.  
  
9. Guarde el archivo .rdlc.  
  
## <a name="next-task"></a>Tarea siguiente  
Ha diseñado correctamente el informe secundario usando el Asistente para informes. Luego, agregará un control ReportViewer a la aplicación de sitio Web. Vea [Lección 6: agregar un control ReportViewer a la aplicación](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md).  
  
  
  

