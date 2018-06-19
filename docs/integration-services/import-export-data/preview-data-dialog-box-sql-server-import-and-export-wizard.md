---
title: Cuadro de diálogo Vista previa de los datos (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f90a8b24e68d225cb929d4139b8efc42642e1a22
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35411557"
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>Cuadro de diálogo Vista previa de los datos (Asistente para importación y exportación de SQL Server)
  Después de especificar los datos que quiere copiar, puede hacer clic en **Vista previa** para abrir el cuadro de diálogo **Vista previa de los datos** . En esta página, puede obtener una vista previa de hasta 200 filas de datos de ejemplo del origen de datos. Esto confirma que el asistente va a copiar los datos que quiere copiar.
  
## <a name="screen-shot-of-the-preview-data-page"></a>Captura de pantalla de la página Vista previa de los datos 
 En la siguiente captura de pantalla se muestra el cuadro de diálogo **Vista previa de los datos** del asistente.  
 
![Página Vista previa de datos del Asistente para importación y exportación](../../integration-services/import-export-data/media/preview-data.png "Preview data page of the Import and Export Wizard")  
  
## <a name="preview-sample-data"></a>Obtener una vista previa de los datos de ejemplo  
 **Source**  
Muestra la consulta que usa el asistente para cargar datos del origen de datos.

Si ha seleccionado una tabla para copiar, el campo **Origen** muestra una consulta `SELECT * FROM <table>` en lugar del nombre de la tabla. 
  
 **Cuadricula de datos de ejemplo**  
 Muestra hasta 200 filas de datos de ejemplo que la consulta devuelve del origen de datos.  


## <a name="thats-not-right-i-want-to-change-something"></a>No es correcto, deseo cambiar algo
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estas modificaciones, haga clic en **Aceptar** para volver a la página **Seleccionar tablas y vistas de origen** y después haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.

## <a name="whats-next"></a>¿Qué sigue?  
 Después de obtener una vista previa de los datos que se van a copiar y de hacer clic en **Aceptar**, el cuadro de diálogo **Vista previa de los datos** devuelve a la página **Seleccionar tablas y vistas de origen** o **Configurar el destino del archivo plano** . Para más información, vea [Seleccionar tablas y vistas de origen](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) o [Configurar el destino del archivo plano](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md).  
 
 ## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
