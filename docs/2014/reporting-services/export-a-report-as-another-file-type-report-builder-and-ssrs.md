---
title: Exportar un informe como otro tipo de archivo (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: b577568b-ecbd-44c3-be88-31dab6fc38a2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6da8c1190c07d3df930a2d83937e3a5ec39da32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109178"
---
# <a name="export-a-report-as-another-file-type-report-builder-and-ssrs"></a>Exportar un informe como otro tipo de archivo (Generador de informes y SSRS)
  Puede representar el informe en otro formato de archivo, como CSV, Imagen, PDF, [!INCLUDE[ofprword](../includes/ofprword-md.md)]o [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)]mientras obtiene una vista previa del mismo en el Generador de informes o el Diseñador de informes, o puede representar el informe mientras lo ve en el servidor de informes. Representar el informe en un formato concreto resulta útil si se desea guardar el informe de manera inmediata como otro tipo de archivo sin publicarlo en el servidor de informes o si se desea ver el aspecto que presentará su diseño cuando se entregue a los lectores en un formato determinado. Representar el informe en el servidor de informes resulta útil si se configuran suscripciones o se entregan informes a través del correo electrónico o si se desea guardar un informe que está disponible en el servidor de informes. Para obtener más información, vea [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-export-a-report-as-another-file-type-in-report-builder"></a>Exportar un informe como otro tipo de archivo en el Generador de informes  
  
1.  Obtenga una vista previa del informe.  
  
2.  En la cinta, haga clic en **Exportar**.  
  
3.  Seleccione el formato que desea usar.  
  
     Se abre el cuadro de diálogo **Guardar como**. De forma predeterminada, aparece el nombre de archivo del informe que exportó. Si lo desea, puede cambiar el nombre de archivo.  
  
4.  Navegue hasta la ubicación donde guardó el informe exportado y ábralo.  
  
> [!NOTE]  
>  Si el programa no puede abrir el informe en el formato que ha elegido porque no tiene un programa asociado a este tipo de archivo, le solicitará que guarde el informe exportado o que busque un programa en línea para abrirlo.  
  
### <a name="to-export-a-report-as-another-file-type-in-report-manager"></a>Para exportar un informe como otro tipo de archivo en el Administrador de informes  
  
1.  En la página **Inicio** del Administrador de informes, navegue hasta el informe que desea exportar.  
  
2.  Haga clic en el informe.  
  
     Se genera el informe.  
  
3.  En la barra de herramientas del Visor de informes, haga clic en la flecha de lista desplegable **Seleccionar un formato** .  
  
4.  Seleccione el formato que desea usar.  
  
5.  Haga clic en **Exportar**.  
  
     Aparece un mensaje preguntándole si desea abrir o guardar el archivo.  
  
6.  Para ver el informe en el formato de exportación seleccionado, haga clic en **Abrir**.  
  
     \- O bien  
  
     Para guardar de manera inmediata el informe en el formato de exportación seleccionado, haga clic en **Guardar**.  
  
     El informe se muestra o se guarda mediante la aplicación asociada al formato elegido. Si hace clic en **Guardar**, se le solicitará una ubicación para guardar el informe.  
  
     **Nota:** Si el programa no puede abrir el informe en el formato que ha elegido porque no tiene un programa asociado a este tipo de archivo, se le pedirá que guarde el informe exportado o que busque un programa en línea para abrir el informe.  
  
### <a name="to-export-a-report-as-another-file-type-in-a-sharepoint-library"></a>Para exportar un informe como otro tipo de archivo en una biblioteca de SharePoint.  
  
1.  Obtenga una vista previa del informe.  
  
2.  En la barra de herramientas, haga clic en **Acciones**, seleccione **Exportar**y, a continuación, seleccione el formato que desea utilizar.  
  
     Se abre el cuadro de diálogo **Descarga de archivos** .  
  
3.  Para ver el informe en el formato de exportación seleccionado, haga clic en **Abrir**.  
  
     \- O bien  
  
     Para guardar de manera inmediata el informe en el formato de exportación seleccionado, haga clic en **Guardar**.  
  
     El informe se muestra o se guarda mediante la aplicación asociada al formato elegido. Si hace clic en **Guardar**, se le solicitará una ubicación para guardar el informe.  
  
     Opcionalmente, cambie el nombre de archivo del informe exportado.  
  
     **Nota:** Si el programa no puede abrir el informe en el formato que ha elegido porque no tiene un programa asociado a este tipo de archivo, se le pedirá que guarde el informe exportado o que busque un programa en línea para abrir el informe.  
  
## <a name="see-also"></a>Consulte también  
 [Exportar informes &#40;Generador de informes y SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)   
 [Paginación en Reporting Services &#40;Generador de informes y SSRS&#41;](report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Funcionalidad interactiva para diferentes extensiones de representación de informes &#40;Generador de informes y SSRS&#41;](report-builder/interactive-functionality-different-report-rendering-extensions.md)  
  
  
