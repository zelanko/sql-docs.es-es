---
title: Obtener una vista previa de los informes
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 21928cd6637815000983e8a0fe05aa4e77d1c216
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "67412972"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>Vista previa de los informes en SQL Server Reporting Services (SSRS)

  Después de diseñar un informe, puede que desee verlo antes de publicarlo en un entorno de producción. Existen varias maneras de verlo: cambiar al modo de vista previa del Diseñador de informes, usar la ventana de vista previa del Diseñador de informes y publicar el informe en un servidor de informes en un entorno de prueba.  
  
> [!NOTE]  
> Cuando se obtiene una vista previa de un informe, los datos de ese informe se almacenan en la caché en un archivo del equipo local. Cuando se obtiene de nuevo una vista previa del mismo informe mediante la misma consulta, los mismos parámetros y las mismas credenciales, el Diseñador de informes recupera la copia en caché en lugar de volver a ejecutar la consulta. El archivo de datos se guarda como * \<nombreinforme>*. RDL. Data en el mismo directorio que el archivo de definición de informe. El archivo no se elimina cuando se cierra el Diseñador de informes.  
  
## <a name="preview-mode"></a>Modo de vista previa

 Puede obtener una vista previa de un informe en Diseñador de informes haciendo clic en **vista previa**. El informe se ejecuta en modo local, utilizando la misma funcionalidad de procesamiento y representación de informes disponible en el servidor de informes. El informe que se muestra es una imagen interactiva; puede seleccionar parámetros, hacer clic en vínculos, ver el mapa del documento, así como expandir y contraer las áreas ocultas del informe. También puede exportar el informe con cualquiera de los formatos de representación instalados.  
  
## <a name="standalone-preview"></a>Vista previa independiente

 También puede obtener una vista previa de un informe si ejecuta el proyecto de informe en una configuración de depuración, por ejemplo, para depurar los ensamblados personalizados que ha escrito. Existen tres modos de ejecutar un proyecto:  
  
- Haciendo clic en **iniciar** en el menú **depurar** .  
  
- Haciendo clic en el botón **iniciar** de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] la barra de herramientas estándar.  
  
- Presionar la tecla F5.  
  
 Si utiliza una configuración de proyecto que genera el informe pero no lo implementa, el informe especificado en la propiedad `StartItem` de la configuración actual se abrirá en una ventana de vista previa distinta. La ventana de vista previa muestra el informe de la misma manera y tiene la misma funcionalidad que el modo de vista previa.  
  
> [!NOTE]  
> Antes de depurar un informe es preciso establecer un elemento de inicio. Para establecer un elemento de inicio, en Explorador de soluciones, haga clic con el botón secundario en **Properties**el proyecto de informe, `StartItem`haga clic en propiedades y, a continuación, en, seleccione el nombre del informe que desea mostrar.  
  
 Si quiere obtener la vista previa de un informe determinado que no es el elemento de inicio del proyecto, seleccione una configuración que genere el informe pero no lo implemente (por ejemplo, la configuración de depuración local), haga clic con el botón derecho en el informe y, luego, haga clic en **Ejecutar**. Debe elegir una configuración que no implemente el informe; de lo contrario, éste se publicará en el servidor de informes en lugar de mostrarse localmente en una ventana de vista previa.  
  
## <a name="print-preview"></a>Vista previa de impresión

 La primera vez que se ve un informe en el modo de vista previa o en la ventana de vista previa, la vista del informe se asemeja a un informe generado mediante la extensión de representación en HTML. La vista previa no es HTML, pero el diseño y la paginación del informe son similares a la salida con formato HTML.  
  
 Para cambiar la vista de manera que represente un informe impreso, cambie al modo de vista previa de impresión. Haga clic en el botón **Vista previa de impresión** de la barra de herramientas de la vista previa. El informe se mostrará como si estuviera en una página física. Esta vista se asemeja a la salida que se obtiene mediante las extensiones de representación en imágenes y en PDF. La vista previa de impresión no es un archivo de imagen ni un archivo PDF, pero el diseño y la paginación del informe son similares a la salida con estos formatos.  
  
## <a name="publish-to-a-test-server"></a>Publicación en un servidor de pruebas

 También puede probar los informes publicándolos en un servidor de pruebas. Publicar un informe en un servidor de pruebas es lo mismo que publicarlo en un servidor de producción. Para más información sobre cómo publicar un informe, vea [Publicar informes en un servidor de informes](publishing-reports-to-a-report-server.md).  
  
## <a name="next-steps"></a>Pasos siguientes

 - [Imprimir informes &#40;Generador de informes y SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)
 - [Imprimir un informe &#40;Generador de informes y SSRS&#41;](../report-builder/print-a-report-report-builder-and-ssrs.md)
 - [Publicar informes](../publish-reports.md)
 - [Usar ensamblados personalizados con informes](../custom-assemblies/using-custom-assemblies-with-reports.md)