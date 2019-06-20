---
title: Guardar informes (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 59ddc4b8-9517-4d3f-9c88-a07e9907cecb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e21b1c9e48dcccf8b72a60fbd381aac3d878c0dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107631"
---
# <a name="saving-reports-report-builder"></a>Guardar informes (Generador de informes)
  En el Generador de informes puede guardar un informe en un servidor de informes, una biblioteca de SharePoint, un recurso compartido de archivos en el que tenga permiso de escritura o su equipo. Puede guardar un informe en la misma ubicación desde la que lo abrió, guardarlo en una ubicación diferente o guardarlo con un nuevo nombre en la misma ubicación o en otra. De forma predeterminada, un informe es vuelve a guardar en la ubicación desde la que se abrió. Al guardar el informe, lo que realmente se guarda es la definición de informe, que describe su diseño. No se guardan los datos. Cada vez que ejecuta el informe, sus datos se actualizan y es probable que sean diferentes a los de antes de la ejecución.  
  
 Si desea guardar el informe en un formato diferente o guardar la definición de informe con los datos, utilice una de las características de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] siguientes:  
  
-   Exporte un informe representado a un formato de archivo diferente, por ejemplo a archivos separados por comas (CSV) o libros de Excel, y guarde el informe en ese formato. También puede generar las fuentes de distribución de datos de los informes y guardar los datos del informe.  
  
-   Cree las suscripciones de informe para entregar y guardar los informes en un recurso compartido de archivos.  
  
-   Utilice el historial de informes para guardar las versiones de los informes representados como copias históricas.  
  
 Para más información sobre cómo ver y administrar informes directamente en el servidor de informes, vea [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md) y [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Libros en pantalla](https://go.microsoft.com/fwlink/?LinkId=154888) en msdn.microsoft.com.  
  
##  <a name="SavingReportDefinitions"></a> Guardar definiciones de informe  
 Aunque puede guardar los informes en su equipo, si se guardan en un servidor de informes, se obtienen muchas ventajas.  
  
 Al guardar un informe en un servidor de informes, se proporcionan las ventajas siguientes:  
  
-   Los informes están disponibles para todos los que tengan permiso de acceso a la carpeta en la que guardaron.  
  
-   Los informes se pueden administrar y ver desde el Administrador de informes.  
  
-   Los recursos de informe como los orígenes de datos, las imágenes y los subinformes están almacenadas en un lugar para facilitar el acceso.  
  
-   Los informes se pueden entregar a otros mediante suscripciones.  
  
-   Los informes se almacenan de forma segura en la base de datos del servidor de informes.  
  
-   Las ejecuciones de informes se pueden registrar y proporcionar información de rendimiento y auditoría.  
  
 La acción de guardar un informe en un servidor de informes también se denomina publicar un informe. Al guardar el informe solo guarda la definición de informe. Cada vez que ejecuta el informe, sus datos se actualizan y es probable que sean diferentes a los de antes de la ejecución. Si desea guardar la definición de informe con los datos, debería utilizar la característica de historial de informe. Con esta característica, una copia del informe se guarda con sus datos.  
  

  
##  <a name="ExportingAndSavingReports"></a> Exportar y guardar informes  
 Si los informes que necesita archivar son pocos, quizás le interese exportar el informe y guardarlo como un archivo. Tras exportar un informe a una aplicación (como PDF o Excel), puede guardarlo como un archivo y colocarlo en un directorio compartido protegido de la red. También puede cargar un informe PDF o Excel guardado como un elemento de recurso si desea conservar todas las copias del informe, independientemente del formato, en la base de datos del servidor de informes. Para obtener más información acerca de cómo exportar un informe, vea [exportar informes &#40;generador de informes y SSRS&#41; ](export-reports-report-builder-and-ssrs.md) y [cargar un archivo o informe &#40;el Administrador de informes&#41;](../reports/upload-a-file-or-report-report-manager.md).  
  

  
##  <a name="UsingFileShareDelivery"></a> Usar la entrega a recursos compartidos de archivos  
 Si son muchos los informes que desea archivar, cree una suscripción que entregue el informe directamente al sistema de archivos. En este caso, debe crear una suscripción para cada informe, elegir una carpeta compartida donde almacenar los informes y definir una programación que determine el momento en el que se creará el archivo. Una vez definida la suscripción, el servidor de informes puede ejecutar el informe en modo desatendido y agregar archivos de informe al archivo mediante la programación que se indique. También puede crear programaciones de un solo uso para archivar informes de forma puntual. Para obtener más información acerca de las suscripciones y la entrega a recursos compartidos de archivos, vea la sección sobre la entrega a recursos compartidos de archivos en Reporting Services en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) en los Libros en pantalla de SQL Server.  
  

  
##  <a name="UsingReportHistory"></a> Usar el historial de informes  
 Puede utilizar también la característica de historial de informe para crear copias históricas. De este modo, puede crear una copia de seguridad de la base de datos del servidor de informes y almacenarla en una ubicación segura para utilizarla posteriormente. Todos los historiales de informes (junto con los informes, elementos de orígenes de datos compartidos, carpetas, suscripciones y programaciones compartidas) se almacenan en la base de datos del servidor de informes. Puede crear una copia de seguridad para conservar una copia permanente del historial de informes y los metadatos, como la información de suscripción que indica los destinatarios de un informe. Para obtener más información, vea cómo administrar el historial de informes en la [documentación de Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) , en los Libros en pantalla de SQL Server.  
  

  
##  <a name="HowTo"></a> Temas de procedimientos  
  
-   [Guardar informes en un servidor de informes &#40;Generador de informes&#41;](save-reports-to-a-report-server-report-builder.md)  
  
-   [Guardar un informe en una biblioteca de SharePoint &#40;Generador de informes&#41;](save-a-report-to-a-sharepoint-library-report-builder.md)  
  
-   [Guardar informes en el equipo &#40;generador de informes&#41;](../save-reports-to-your-computer-report-builder.md)  
  

  
## <a name="see-also"></a>Vea también  
 [Informes, elementos de informe y definiciones de informe &#40;Generador de informes y SSRS&#41;](../report-design/reports-report-parts-and-report-definitions-report-builder-and-ssrs.md)   
 [Instalar, desinstalar y asistencia del generador de informes](../install-uninstall-and-report-builder-support.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar informes &#40;generador de informes y SSRS&#41;](export-reports-report-builder-and-ssrs.md)   
 [Imprimir informes &#40;Generador de informes y SSRS&#41;](print-reports-report-builder-and-ssrs.md)  
  
  
