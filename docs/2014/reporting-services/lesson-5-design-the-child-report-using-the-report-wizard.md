---
title: 'Lección 5: Diseñar el informe secundario usando el Asistente para informes | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fd86b5b8b6466f6075f2b3c8814fb13a8ec62d9a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59959931"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lección 5: Diseño del informe secundario usando el Asistente para informes
  Después de crear una conexión de datos y una tabla de datos para el informe secundario, el paso siguiente consiste en diseñar dicho informe usando el Asistente para informes del Diseñador de informes. Para más información sobre el Diseñador de informes, vea [Diseñar informes con el Diseñador de informes &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Para diseñar el informe secundario usando el Asistente para informes  
  
1.  Asegúrese de que el sitio web de nivel superior está seleccionado en el **Explorador de soluciones**.  
  
2.  Haga clic con el botón derecho en el sitio web y seleccione **Agregar nuevo elemento**.  
  
3.  En el **Agregar nuevo elemento** cuadro de diálogo, haga clic en **Asistente para informes**, escriba un nombre para el archivo de informe y, a continuación, haga clic en **agregar**.  
  
     Así se inicia el Asistente para informes.  
  
4.  En el **las propiedades del conjunto de datos** página, en el **origen de datos** cuadro, haga clic en **DataSet2**.  
  
     El cuadro **Conjuntos de datos disponibles** se actualiza automáticamente con el elemento DataTable que ha creado.  
  
5.  Haga clic en **Siguiente**.  
  
6.  En la página **Organizar campos** , haga lo siguiente:  
  
    1.  Arrastre **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**y **StockedQty** desde **Campos disponibles** hasta el cuadro **Valores** .  
  
    2.  Haga clic en la flecha situada junto a **SUM (ProductID)**, **SUM (purchaseorderid)**, **SUM (purchaseorderdetailid)**, **SUM (OrderQty)**,  **SUM (receivedqty)**, **SUM (rejectedqty)**, y **SUM (stockedqty)** y desactive el **suma** selección.  
  
7.  Haga clic en **siguiente** dos veces y, a continuación, haga clic en **finalizar** para cerrar el **Asistente para informes**.  
  
     Ahora ha creado el archivo .rdlc. El archivo se abre en el Diseñador de informes. El Tablix que se diseñó se muestra en la superficie de diseño.  
  
8.  Con el archivo .rdlc abierto, agregue un parámetro haciendo lo siguiente:  
  
    1.  Haga clic en **parámetros** en el **datos de informe** panel y, a continuación, haga clic en **agregar parámetros**.  
  
    2.  Escriba **productid** en el cuadro **Nombre** .  
  
    3.  Confirme que **Entero** está seleccionado en el cuadro de lista **Tipo de datos** .  
  
    4.  Haga clic en **Aceptar**.  
  
9. Guarde el archivo .rdlc.  
  
## <a name="next-task"></a>Tarea siguiente  
 Ha diseñado correctamente el informe secundario usando el Asistente para informes. Luego, agregará un control ReportViewer a la aplicación de sitio Web.  
  
  
