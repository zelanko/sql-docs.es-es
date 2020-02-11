---
title: Cuadro de diálogo Propiedades de la acción (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.action.f1
- "10413"
- "10504"
- sql12.rtp.rptdesigner.calculatedseriesproperties.action.f1
- sql12.rtp.rptdesigner.pictureproperties.action.f1
- sql12.rtp.rptdesigner.actionproperties.f1
- sql12.rtp.rptdesigner.charttitleproperties.action.f1
- "10133"
- "10052"
- "10147"
- sql12.rtp.rptdesigner.chartproperties.action.f1
- "10122"
- sql12.rtp.rptdesigner.serieslabelproperties.action.f1
- sql12.rtp.rptdesigner.textboxproperties.action.f1
- "10162"
- "10168"
- sql12.rtp.rptdesigner.textproperties.action.f1
- sql12.rtp.rptdesigner.placeholderproperties.action.f1
- "10250"
- "10129"
- "10244"
- sql12.rtp.rptdesigner.seriesproperties.action.f1
ms.assetid: 2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3d6069d5720121b02c627528ec772cb61ddb0a10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66110078"
---
# <a name="action-properties-dialog-box-report-builder-and-ssrs"></a>Cuadro de diálogo Propiedades de acción (Generador de informes y SSRS)
  El cuadro de diálogo **Acción** se puede usar para habilitar las opciones de hipervínculo para los elementos de gráfico, medidor y mapa que admitan vínculos. Defina una acción para que un usuario pueda hacer clic en el informe y vincularse a una dirección URL, a un informe diferente en el mismo servidor de informes o a un sitio de SharePoint integrado con un servidor de informes, o a una ubicación diferente del mismo informe.  
  
## <a name="options"></a>Opciones  
 **Habilitar como una acción**  
 Seleccione una opción para indicar la acción que tendrá lugar cuando el usuario haga clic en el elemento.  
  
 **None**  
 Elija esta opción para indicar que el elemento no tiene ninguna acción.  
  
 **Ir al informe**  
 Elija esta opción para crear un vínculo a un informe detallado que se encuentra en un servidor de informes. Al seleccionar **Ir a informe**, aparecen las siguientes opciones adicionales.  
  
 **Especificar un informe**  
 Escriba o seleccione el nombre del informe que desea utilizar como informe detallado. Los informes detallados deben estar en el mismo servidor de informes que este informe.  
  
 En el caso de un informe publicado en un servidor de informes configurado para el modo nativo, use una ruta de acceso completa o relativa sin la extensión del nombre de archivo. Si el informe se encuentra en la misma carpeta que el actual, use solo el nombre del informe. Si el informe está en una carpeta diferente del mismo servidor de informes, use una ruta de acceso relativa o una ruta de acceso completa. Una ruta de acceso relativa comienza en la carpeta actual y sube por la jerarquía de carpetas, por ejemplo, ../Carpeta2/Informe1. Una ruta de acceso completa se inicia en /, la carpeta Inicio. Por ejemplo, /Informes/Informe1.  
  
 En el caso de un informe publicado en un servidor de informes configurado en el modo integrado de SharePoint, utilice una dirección URL completa, incluida la extensión del nombre de archivo (.rdl). Por ejemplo, http://*\<SharePointservername>/\<site>*/Documents/Report1.RDL. No se admiten las rutas de acceso relativas.  
  
 Para obtener más información, vea [Especificar las rutas de acceso a los elementos externos &#40;Generador de informes y SSRS&#41;](report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md) en la [la documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
 **Usar estos parámetros para ejecutar el informe**  
 Agregue una lista de parámetros para pasárselos al informe detallado. Los nombres de los parámetros deben coincidir con los de los parámetros definidos para el informe de destino. Use los botones **Agregar** y **Eliminar** para agregar y quitar parámetros, y las flechas hacia arriba y hacia abajo para ordenar la lista de parámetros.  
  
 **Add (Agregar)**  
 Agregue un nuevo parámetro para pasárselo al informe detallado.  
  
 **Eliminar**  
 Elimina un parámetro del informe detallado.  
  
 **Flecha arriba**  
 Mueve el parámetro hacia arriba en la lista.  
  
 **Flecha abajo**  
 Mueve el parámetro hacia abajo en la lista.  
  
 **Nombre**  
 Escriba el nombre de un parámetro definido en el informe detallado.  
  
 **Valor**  
 Escriba o seleccione el valor que debe pasarse al parámetro especificado para el informe detallado. Haga clic en el botón **expresión** (*FX*) para editar la expresión.  
  
 **Omitir**  
 Seleccione esta opción para impedir que el parámetro se ejecute. De forma predeterminada, esta casilla está desactivada. Para activar la casilla, haga clic en el botón **expresión** (*FX*) y escriba **true** o cree una expresión. La casilla se activa al hacer clic en **Aceptar** en el cuadro de diálogo **expresión** .  
  
 **Ir a marcador**  
 Elija esta opción para definir un vínculo a un marcador en el informe actual. Al seleccionar **Ir a marcador**, aparece la siguiente opción adicional.  
  
 **Seleccionar marcador**  
 Escriba o seleccione el identificador de marcador al que debe saltar el informe cuando el usuario haga clic en el vínculo. Haga clic en el botón expresión (**FX**) para cambiar la expresión. El identificador de marcador puede ser un identificador estático o una expresión que se evalúa como un identificador de marcador. La expresión puede incluir un campo que contenga un identificador de marcador.  
  
 Para crear un vínculo a un marcador, debe definir primero la propiedad Bookmark de un elemento de informe. Para definir la propiedad Bookmark, seleccione un elemento de informe y en el panel Propiedades, escriba un valor o expresión para el identificador de marcador; por ejemplo, SalesChart o 5TopSales.  
  
 **Ir a dirección URL**  
 Elija esta opción para definir un vínculo a una página web. Escriba o seleccione la dirección URL de una página web o una expresión que se evalúe como la dirección URL de una página web. Haga clic en el botón **expresión** (*FX*) para cambiar la expresión. Esta expresión puede incluir un campo que contenga una dirección URL. Al seleccionar **Ir a dirección URL**, aparece la siguiente opción adicional.  
  
 **Seleccionar dirección URL**  
 Escriba o especifique la dirección URL del elemento. En el caso de un elemento publicado en un servidor de informes configurado para el modo nativo, use una ruta de acceso completa o relativa. Por ejemplo, http://*\<ServerName>*/images/image1.jpg. En el caso de un elemento publicado en un servidor de informes configurado en el modo integrado de SharePoint, use una dirección URL completa (por ejemplo, http://*\<SharePointservername>/\<site>*/Documents/images/image1.jpg).  
  
## <a name="see-also"></a>Consulte también  
 [Gráficos &#40;Generador de informes y SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [Generador de informes ayuda para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Agregar un subinforme y parámetros &#40;Generador de informes y SSRS&#41;](report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
  
