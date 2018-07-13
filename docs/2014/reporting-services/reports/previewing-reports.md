---
title: Obtener la vista previa de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Report Designer [Reporting Services], previewing reports
- previewing reports [Reporting Services]
- printing previews
- test servers [Reporting Services]
ms.assetid: 85117f6c-828e-45c9-810f-e700d9bfba67
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: afcfb2cf31526f4e8898fafbe72f9492a1848886
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202535"
---
# <a name="previewing-reports"></a>Obtener la vista previa de informes
  Después de diseñar un informe, puede que desee verlo antes de publicarlo en un entorno de producción. Existen varias maneras de verlo: cambiar al modo de vista previa del Diseñador de informes, usar la ventana de vista previa del Diseñador de informes y publicar el informe en un servidor de informes en un entorno de prueba.  
  
> [!NOTE]  
>  Cuando se obtiene una vista previa de un informe, los datos de ese informe se almacenan en la caché en un archivo del equipo local. Cuando se obtiene de nuevo una vista previa del mismo informe mediante la misma consulta, los mismos parámetros y las mismas credenciales, el Diseñador de informes recupera la copia en caché en lugar de volver a ejecutar la consulta. El archivo de datos se guarda como *\<nombreDeInforme>*.rdl.data en el mismo directorio que el archivo de definición de informe. El archivo no se elimina cuando se cierra el Diseñador de informes.  
  
## <a name="preview-mode"></a>Modo de vista previa  
 Puede obtener una vista previa un informe en el Diseñador de informes, haga clic en **Preview**. El informe se ejecuta en modo local, utilizando la misma funcionalidad de procesamiento y representación de informes disponible en el servidor de informes. El informe que se muestra es una imagen interactiva; puede seleccionar parámetros, hacer clic en vínculos, ver el mapa del documento, así como expandir y contraer las áreas ocultas del informe. También puede exportar el informe con cualquiera de los formatos de representación instalados.  
  
## <a name="standalone-preview"></a>Vista previa independiente  
 También puede obtener una vista previa de un informe si ejecuta el proyecto de informe en una configuración de depuración, por ejemplo, para depurar los ensamblados personalizados que ha escrito. Existen tres modos de ejecutar un proyecto:  
  
-   Al hacer clic en **iniciar** en el **depurar** menú.  
  
-   Al hacer clic en el **iniciar** situado en el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] barra de herramientas estándar.  
  
-   Presionar la tecla F5.  
  
 Si usa una configuración de proyecto que genera el informe pero no lo implementa, el informe que se especifica en el `StartItem` propiedad de la configuración actual se abre en una ventana de vista previa independiente. La ventana de vista previa muestra el informe de la misma manera y tiene la misma funcionalidad que el modo de vista previa.  
  
> [!NOTE]  
>  Antes de depurar un informe es preciso establecer un elemento de inicio. Para establecer un elemento de inicio, en el Explorador de soluciones, haga clic en el proyecto de informe, haga clic en **propiedades**y, a continuación, en `StartItem`, seleccione el nombre del informe para mostrar.  
  
 Si quiere obtener la vista previa de un informe determinado que no es el elemento de inicio del proyecto, seleccione una configuración que genere el informe pero no lo implemente (por ejemplo, la configuración de depuración local), haga clic con el botón derecho en el informe y, luego, haga clic en **Ejecutar**. Debe elegir una configuración que no implemente el informe; de lo contrario, éste se publicará en el servidor de informes en lugar de mostrarse localmente en una ventana de vista previa.  
  
## <a name="print-preview"></a>Vista previa de impresión  
 La primera vez que se ve un informe en el modo de vista previa o en la ventana de vista previa, la vista del informe se asemeja a un informe generado mediante la extensión de representación en HTML. La vista previa no es HTML, pero el diseño y la paginación del informe son similares a la salida con formato HTML.  
  
 Para cambiar la vista de manera que represente un informe impreso, cambie al modo de vista previa de impresión. Haga clic en el botón **Vista previa de impresión** de la barra de herramientas de la vista previa. El informe se mostrará como si estuviera en una página física. Esta vista se asemeja a la salida que se obtiene mediante las extensiones de representación en imágenes y en PDF. La vista previa de impresión no es un archivo de imagen ni un archivo PDF, pero el diseño y la paginación del informe son similares a la salida con estos formatos.  
  
## <a name="publishing-to-a-test-server"></a>Publicar en un servidor de pruebas  
 También puede probar los informes publicándolos en un servidor de pruebas. Publicar un informe en un servidor de pruebas es lo mismo que publicarlo en un servidor de producción. Para más información sobre cómo publicar un informe, vea [Publicar informes en un servidor de informes](publishing-reports-to-a-report-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Imprimir informes &#40;Generador de informes y SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)   
 [Imprimir un informe &#40;Generador de informes y SSRS&#41;](../report-builder/print-a-report-report-builder-and-ssrs.md)   
 [Publicar informes](../publish-reports.md)   
 [Uso de ensamblados personalizados con informes](../custom-assemblies/using-custom-assemblies-with-reports.md)  
  
  
