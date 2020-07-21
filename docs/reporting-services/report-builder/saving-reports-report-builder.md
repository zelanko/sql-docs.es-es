---
title: Guardar informes (Generador de informes) | Microsoft Docs
description: En el Generador de informes, puede guardar la definición de un informe, que incluye el diseño, pero no los datos. Los datos se actualizan cada vez que se ejecuta el informe.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9c96b1a65c6a576391f072f2bdabb4b70cb0fd63
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290790"
---
# <a name="saving-reports-report-builder"></a>Guardar informes (Generador de informes)
  En el Generador de informes puede guardar un informe pagina en un servidor de informes de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , una biblioteca de SharePoint, un recurso compartido de archivos en el que tenga permiso de escritura o en su equipo. 
  
Cuando guarda un informe, lo que realmente se guarda es la definición de informe, que describe su diseño. No se guardan los datos. Cada vez que ejecuta el informe, sus datos se actualizan y es probable que sean diferentes a los de antes de la ejecución.  
  
 Si desea guardar el informe en un formato diferente o guardar la definición de informe con los datos, utilice una de las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] siguientes:  
  
-   Exporte un informe representado a un formato de archivo diferente, por ejemplo a archivos separados por comas (CSV) o libros de Excel, y guarde el informe en ese formato. También puede generar las fuentes de distribución de datos de los informes y guardar los datos del informe.  
  
-   Cree las suscripciones de informe para entregar y guardar los informes en un recurso compartido de archivos.  
  
-   Utilice el historial de informes para guardar las versiones de los informes representados como copias históricas.  
  
 Para más información sobre cómo ver y administrar informes directamente en el servidor de informes, consulte [Buscar, ver y administrar informes &#40;Generador de informes y SSRS &#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md) y [Servidor de informes de Reporting Services &#40;Modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md).  
  
##  <a name="saving-reports-to-a-report-server"></a><a name="SavingReportDefinitions"></a> Guardar informes en un servidor de informes  
  La acción de guardar un informe en un servidor de informes también se denomina publicar un informe. Aunque puede guardar los informes en su equipo, si se guardan en un servidor de informes, se obtienen muchas ventajas:  
  
-   Los informes están disponibles para todos los que tengan permiso de acceso a la carpeta en la que guardaron.  
  
-   Los informes se pueden administrar y ver en el portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Los recursos de informe como los orígenes de datos, las imágenes y los subinformes están almacenadas en un lugar para facilitar el acceso.  
  
-   Los informes se pueden entregar a otros mediante suscripciones.  
  
-   Los informes se almacenan de forma segura en la base de datos del servidor de informes.  
  
-   Las ejecuciones de informes se pueden registrar y proporcionar información de rendimiento y auditoría.  
  
##  <a name="exporting-and-saving-reports"></a><a name="ExportingAndSavingReports"></a> Exportar y guardar informes  
 Si los informes que necesita archivar son pocos, quizás le interese exportar el informe y guardarlo como un archivo. Tras exportar un informe a una aplicación (como PDF o Excel), puede guardarlo como un archivo y colocarlo en un directorio compartido protegido de la red. También puede cargar un informe PDF o Excel guardado como un elemento de recurso si desea conservar todas las copias del informe, independientemente del formato, en la base de datos del servidor de informes. Para más información sobre cómo exportar un informe, consulte [Exportar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md) y [Cargar un archivo o informe](../../reporting-services/reports/upload-a-file-or-report-report-manager.md).  
  
##  <a name="using-file-share-delivery"></a><a name="UsingFileShareDelivery"></a> Usar la entrega a recursos compartidos de archivos  
 Si son muchos los informes que desea archivar, cree una suscripción que entregue el informe directamente al sistema de archivos. En este caso, debe crear una suscripción para cada informe, elegir una carpeta compartida donde almacenar los informes y definir una programación que determine el momento en el que se creará el archivo. Una vez definida la suscripción, el servidor de informes puede ejecutar el informe en modo desatendido y agregar archivos de informe al archivo mediante la programación que se indique. También puede crear programaciones de un solo uso para archivar informes de forma puntual. Para más información sobre las suscripciones y la entrega a recursos compartidos de archivos, consulte [Entrega a recursos compartidos de archivos en Reporting Services](../../reporting-services/subscriptions/file-share-delivery-in-reporting-services.md).  
  
##  <a name="using-report-history"></a><a name="UsingReportHistory"></a> Usar el historial de informes  
 Puede utilizar también la característica de historial de informe para crear copias históricas. De este modo, puede crear una copia de seguridad de la base de datos del servidor de informes y almacenarla en una ubicación segura para utilizarla posteriormente. Todos los historiales de informes (junto con los informes, elementos de orígenes de datos compartidos, carpetas, suscripciones y programaciones compartidas) se almacenan en la base de datos del servidor de informes. Puede crear una copia de seguridad para conservar una copia permanente del historial de informes y los metadatos, como la información de suscripción que indica los destinatarios de un informe. Para obtener más información, vea [Crear, modificar y eliminar instantáneas del historial de informes](../../reporting-services/report-server/create-modify-and-delete-snapshots-in-report-history.md).  
 
##  <a name="how-to-topics"></a><a name="HowTo"></a> Temas de procedimientos  
  
-   [Guardar informes en un servidor de informes &#40;Generador de informes&#41;](../../reporting-services/report-builder/save-reports-to-a-report-server-report-builder.md)  
  
-   [Guardar un informe en una biblioteca de SharePoint &#40;Generador de informes&#41;](../../reporting-services/report-builder/save-a-report-to-a-sharepoint-library-report-builder.md)  
   
## <a name="see-also"></a>Consulte también  
 [Informes, elementos de informe y definiciones de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Install Report Builder](../install-windows/install-report-builder.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportación de informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)   
 [Imprimir informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)  
  
  
