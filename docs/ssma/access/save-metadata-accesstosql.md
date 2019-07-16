---
title: Guardar metadatos (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: fa4ce8ad-9935-4195-90f9-3fdac587a4ee
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: f987e03ad8dda27e436f22ef54fc3c2646579f4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051548"
---
# <a name="save-metadata-accesstosql"></a>Guardar metadatos (AccessToSQL)
El **guardar metadatos** cuadro de diálogo le pide que cargar los metadatos en su proyecto SSMA antes de guardarlo. Esto le permite tener un archivo de proyecto completo que se puede usar sin conexión y enviar a otras personas, como el personal de soporte técnico.  
  
Para tener acceso a la **guardar metadatos** cuadro de diálogo, guarde el proyecto. Si falta cualquier metadato SSMA mostrará el **guardar metadatos** cuadro de diálogo.  
  
## <a name="options"></a>Opciones  
**Name**  
El nombre de cada base de datos en el proyecto.  
  
**Estado**  
Indica si los metadatos se cargan en el proyecto SSMA, o si faltan metadatos.  
  
SSMA carga los metadatos en el proyecto según sea necesario. Los metadatos se cargan automáticamente al examinar los metadatos y convertir los esquemas.  
  
**Seleccionar todo**  
Selecciona todas las bases de datos.  
  
**Desactivar**  
Borra la casilla de verificación para todas las bases de datos donde faltan metadatos. No desactive la casilla de verificación si se ha cargado los metadatos.  
  
**Guardar**  
Guarda el proyecto, cargar los metadatos para las bases de datos seleccionadas que faltan metadatos.  
  
**Cancelar**  
Cancela la operación de guardar operación. Los metadatos que faltan no se cargan en el proyecto.  
  
