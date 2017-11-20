---
title: "Obtener una vista previa de los datos de cuadro de diálogo (SQL Server importar y exportar) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: import-export-data
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bfa75d2c1d2d50d1f0205fed22811ddbb3b96747
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>Cuadro de diálogo Vista previa de los datos (Asistente para importación y exportación de SQL Server)
  Después de especificar los datos que quiere copiar, puede hacer clic en **Vista previa** para abrir el cuadro de diálogo **Vista previa de los datos** . En esta página, puede obtener una vista previa de hasta 200 filas de datos de ejemplo del origen de datos. Esto confirma que el asistente va a copiar los datos que quiere copiar.
  
## <a name="screen-shot-of-the-preview-data-page"></a>Captura de pantalla de la página Vista previa de los datos 
 En la siguiente captura de pantalla se muestra el cuadro de diálogo **Vista previa de los datos** del asistente.  
 
![Página de datos de vista previa de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/preview-data.png "página de datos de vista previa de la importación y el Asistente para exportación")  
  
## <a name="preview-sample-data"></a>Obtener una vista previa de los datos de ejemplo  
 **Origen**  
Muestra la consulta que usa el asistente para cargar datos del origen de datos.

Si ha seleccionado una tabla que se copia, la **origen** campo muestra un `SELECT * FROM <table>` consulta en lugar del nombre de tabla. 
  
 **Cuadricula de datos de ejemplo**  
 Muestra hasta 200 filas de datos de ejemplo que la consulta devuelve del origen de datos.  


## <a name="thats-not-right-i-want-to-change-something"></a>No es correcto, que desea cambiar algo
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estos cambios, haga clic en **Aceptar** para volver a la **seleccionar tablas de origen y vistas** página y, a continuación, haga clic en **volver** para volver a las páginas anteriores, donde puede cambiar el selecciones.

## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de obtener una vista previa de los datos que se van a copiar y de hacer clic en **Aceptar**, el cuadro de diálogo **Vista previa de los datos** devuelve a la página **Seleccionar tablas y vistas de origen** o **Configurar el destino del archivo plano** . Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

