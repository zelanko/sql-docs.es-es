---
title: Agregar, cambiar o eliminar parámetros de informe (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d1c11541a449299f1dce55e720c7d882b3a70089
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294483"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>Agregar, cambiar o eliminar parámetros de informe (Generador de informes y SSRS)
  Los parámetros de informe permiten elegir datos de informe, conectar informes relacionados y cambiar la presentación de los informes. Puede proporcionar un valor predeterminado y una lista de valores disponibles, y el usuario puede cambiar la selección.  
  
 Una vez publicado el informe, puede cambiar los valores predeterminados, los valores disponibles y otras propiedades del parámetro en el servidor de informes. Puede proporcionar varios conjuntos de valores de parámetros predeterminados creando informes vinculados. Para más información, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
 Este artículo trata sobre la incorporación de parámetros de informes a un informe paginado en [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] o el Diseñador de informes de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede agregar parámetros de informes a informes móviles en  [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]. Consulte [Create mobile reports with SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md) para obtener más información.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>Para agregar o modificar un parámetro de informe  
  
1.  En [!INCLUDE[ssRBnoversion](../../includes/ssrbnoversion.md)] o en el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], en el panel **Datos de informe** , haga clic con el botón derecho en el nodo **Parámetros** y haga clic en **Agregar parámetro**. Se abrirá el cuadro de diálogo **Propiedades de parámetro de informe** .  
  
2.  En **Nombre**, escriba el nombre del parámetro o acepte el nombre predeterminado.  
  
3.  En **Pedir datos**, escriba el texto que se mostrará junto al cuadro de texto del parámetro cuando el usuario ejecute el informe.  
  
4.  En **Tipo de datos**, seleccione el tipo de datos del valor del parámetro.  
  
5.  Si el parámetro puede contener un valor en blanco, seleccione **Permitir valor en blanco**.  
  
6.  Si el parámetro puede contener un valor NULL, seleccione **Permitir valor NULL**.  
  
7.  Para permitir a los usuarios seleccionar más de un valor para el parámetro, seleccione **Permitir varios valores**.  
  
8.  Establezca la opción de visibilidad.  
  
    -   Para mostrar el parámetro en la barra de herramientas de la parte superior del informe, seleccione **Visible**.  
  
    -   Para ocultar el parámetro con objeto de que no se muestre en la barra de herramientas, seleccione **Oculto**.  
  
    -   Para ocultar el parámetro y evitar que pueda modificarse en el servidor de informes una vez publicado el informe, seleccione **Interno**. De esta forma, el parámetro de informe solamente podrá verse en la definición de informe. Si elige esta opción, debe establecer un valor predeterminado o permitir que el parámetro acepte un valor NULL.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>Para eliminar un parámetro de informe  
  
1.  En el panel **Datos de informe** , expanda el nodo **Parámetros** .  
  
2.  Haga clic con el botón derecho en el parámetro de informe y, después, haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Consulte también  
 [Agregar, cambiar o eliminar los valores disponibles para un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md)   
 [Agregar, cambiar o eliminar valores predeterminados para un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Cambiar el orden de un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar parámetros en cascada a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: Agregar un parámetro a un informe &#40;Generador de informes&#41;](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [Agregar filtros de conjunto de datos, filtros de región de datos y filtros de grupo &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Usar referencias a la colección de parámetros &#40;generador de informes y SSRS&#41;](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Agregar un parámetro de varios valores a un informe](../../reporting-services/report-design/add-a-multi-value-parameter-to-a-report.md)  
  
  
