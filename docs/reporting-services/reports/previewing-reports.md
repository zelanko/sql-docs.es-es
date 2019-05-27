---
title: Obtener una vista previa de los informes
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 6bd9a273347aa2010cf670ea3a87622e92d69f82
ms.sourcegitcommit: 57c3b07cba5855fc7b4195a0586b42f8b45c08c2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/20/2019
ms.locfileid: "65935892"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>Vista previa de los informes en SQL Server Reporting Services (SSRS)

  Después de diseñar un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], es posible que quiera verlo antes de publicarlo en un entorno de producción. Existen varias maneras de verlo: cambiar al modo de vista previa del Diseñador de informes, usar la ventana de vista previa del Diseñador de informes y publicar el informe en un servidor de informes en un entorno de prueba.  
  
> [!NOTE]  
> Cuando se obtiene una vista previa de un informe, los datos de ese informe se almacenan en la caché en un archivo del equipo local. Cuando se obtiene de nuevo una vista previa del mismo informe mediante la misma consulta, los mismos parámetros y las mismas credenciales, el Diseñador de informes recupera la copia en caché en lugar de volver a ejecutar la consulta. El archivo de datos se guarda como *\<nombreDeInforme>* .rdl.data en el mismo directorio que el archivo de definición de informe. El archivo no se elimina cuando se cierra el Diseñador de informes.  
  
## <a name="preview-mode"></a>Modo de vista previa

 Para obtener una vista previa del informe en el Diseñador de informes, haga clic en ![ssrs_ssdt_preview](../../reporting-services/media/ssrs-ssdt-preview.png "ssrs_ssdt_preview"). El informe se ejecuta en modo local, utilizando la misma funcionalidad de procesamiento y representación de informes disponible en el servidor de informes. El informe que se muestra es una imagen interactiva; puede seleccionar parámetros, hacer clic en vínculos, ver el mapa del documento, así como expandir y contraer las áreas ocultas del informe. También puede exportar el informe con cualquiera de los formatos de representación instalados.  
  
## <a name="standalone-preview"></a>Vista previa independiente

 También puede obtener una vista previa de un informe si ejecuta el proyecto de informe en una configuración de depuración, por ejemplo, para depurar los ensamblados personalizados que ha escrito. El informe se abre en el explorador predeterminado. Existen tres modos de ejecutar un proyecto:  
  
- Hacer clic en **Iniciar depuración** en el menú **Depurar** .  
  
- Hacer clic en el botón **Inicio** de la barra de herramientas estándar de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ![ssrs_ssdt_startdebug](../../reporting-services/reports/media/ssrs-ssdt-startdebug.png "ssrs_ssdt_startdebug").  
  
- Pulsar **F5**.  
  
 Si utiliza una configuración de proyecto que genera el informe pero no lo implementa, el informe especificado en la propiedad **StartItem** de la configuración actual se abrirá en una ventana de vista previa distinta. La ventana de vista previa muestra el informe de la misma manera y tiene la misma funcionalidad que el modo de vista previa.  
  
> [!NOTE]  
> Antes de depurar un informe es preciso establecer un elemento de inicio. Por ejemplo, si ejecuta el modo de depuración y el explorador abre la página principal del servidor de informes y no el informe en modo de vista previa. Para establecer un elemento de inicio, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto de informe, haga clic en **Propiedades**y, luego, en **StartItem**, seleccione el nombre del informe que quiere mostrar.  
  
 Si quiere obtener la vista previa de un informe determinado que no es el elemento de inicio del proyecto, seleccione una configuración que genere el informe pero no lo implemente (por ejemplo, la configuración de depuración local), haga clic con el botón derecho en el informe y, luego, haga clic en **Ejecutar**. Debe elegir una configuración que no implemente el informe; de lo contrario, éste se publicará en el servidor de informes en lugar de mostrarse localmente en una ventana de vista previa.  
  
## <a name="publish-to-a-test-server"></a>Publicación en un servidor de pruebas

 También puede probar los informes si los publica en un servidor de pruebas, va al informe y obtiene una vista previa. Publicar un informe en un servidor de pruebas es lo mismo que publicarlo en un servidor de producción. Para más información sobre cómo publicar un informe, vea [Publicar informes en un servidor de informes](../../reporting-services/reports/publishing-reports-to-a-report-server.md).  
  
## <a name="next-steps"></a>Pasos siguientes

 - [Imprimir informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-reports-report-builder-and-ssrs.md)
 - [Imprimir un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/print-a-report-report-builder-and-ssrs.md)
 - [Publicar informes](https://msdn.microsoft.com/library/ef5a514e-e818-4041-a8b0-15835f9a046b)
 - [Uso de ensamblados personalizados con informes](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)