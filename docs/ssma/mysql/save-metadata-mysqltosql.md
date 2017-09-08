---
title: Guardar metadatos (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9bc6273f-e8b1-430b-81a5-14330a783562
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e4256f90198c87440bbc49ca907867cd029d5c0e
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="save-metadata--mysqltosql"></a>Guardar metadatos (MySQLToSQL)
El **guardar metadatos** cuadro de diálogo le pregunta si desea cargar los metadatos en el proyecto SSMA antes de guardarla. Esto permite tener un archivo de proyecto completo que se puede utilizar sin conexión y enviar a otras personas, como el personal de soporte técnico.  
  
Para tener acceso a la **guardar metadatos** cuadro de diálogo, guarde el proyecto. Si los metadatos no están presente, SSMA mostrará el **guardar metadatos** cuadro de diálogo.  
  
## <a name="options"></a>Opciones  
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
  

