---
title: Guardar metadatos (OracleToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-oracle
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9e49c25f-9216-43f4-8e99-2eaab298e215
caps.latest.revision: "3"
author: Shamikg
ms.author: Shamikg
manager: v-pelars
ms.workload: Inactive
ms.openlocfilehash: 0474407ed9115d059fd25fd9f78aaf1ff7fd02f7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="save-metadata--oracletosql"></a>Guardar metadatos (OracleToSQL)
El **guardar metadatos** cuadro de diálogo le pregunta si desea cargar los metadatos en el proyecto SSMA antes de guardarla. Esto permite tener un archivo de proyecto completo que se puede utilizar sin conexión y enviar a otras personas, como el personal de soporte técnico.  
  
Para tener acceso a la **guardar metadatos** cuadro de diálogo, guarde el proyecto. Si los metadatos no están presente, SSMA mostrará el **guardar metadatos** cuadro de diálogo.  
  
## <a name="options"></a>.  
**Nombre**  
El nombre de cada base de datos en el proyecto.  
  
**Estado**  
Indica si los metadatos se cargan en el proyecto SSMA, o si hay metadatos que faltan.  
  
SSMA carga los metadatos en el proyecto según sea necesario. Metadatos se cargan automáticamente al examinar los metadatos y convertir esquemas.  
  
**Seleccionar todo**  
Selecciona todas las bases de datos.  
  
**Desactivar**  
Borra la casilla de verificación para todas las bases de datos que le faltan metadatos. No puede desactivar la casilla de verificación si se ha cargado un metadatos.  
  
**Guardar**  
Guarda el proyecto, cargar los metadatos de las bases de datos seleccionado que les faltan metadatos.  
  
**Cancelar**  
Cancela la operación de guardar operación. Metadatos que faltan no se cargan en el proyecto.  
  
