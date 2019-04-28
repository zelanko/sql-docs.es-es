---
title: Guardar metadatos (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b2517735-dd19-449f-8cee-08e68ca89d3a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8bfe338c128ce301e98346d17ce00b973912ffd4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667522"
---
# <a name="save-metadata--sybasetosql"></a>Guardar metadatos (SybaseToSQL)
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
  
