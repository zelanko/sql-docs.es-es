---
title: Opciones (diseñadores-Table y página diseñadores de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4a324f7e0bd9ca0d71b727dd109f8d7dd0a8aec7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37240285"
---
# <a name="options-designers-table-and-database-designers-page"></a>Opciones (diseñadores-Table y página diseñadores de base de datos)
  Utilice esta página para determinar el comportamiento predeterminado del diseñador. Para tener acceso a esta configuración, en el menú **Herramientas** , haga clic en **Opciones**, expanda la carpeta **Diseñadores** y haga clic en **Diseñador de tablas**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Sobrescribir el valor de tiempo de espera de la cadena de conexión para actualizaciones del diseñador de tabla**  
 Permite establecer un nuevo valor de tiempo de espera para las acciones del diseñador de tablas. Esto puede resultar útil si el diseñador de tablas afecta a una tabla grande y requiere más tiempo para completar la modificación.  
  
 **Tiempo de espera de transacción después de**  
 Establece un valor de tiempo de espera para el diseñador de tablas.  
  
 **Generar automáticamente Scripts de cambio**  
 Crea automáticamente un script para implementar los cambios definidos en el diseñador de tablas.  
  
 **Advertir si existen claves principales nulas**  
 Presenta un cuadro de diálogo de advertencia cuando un campo seleccionado para una clave principal puede contener valores NULL.  
  
 **Advertir sobre detección de diferencias**  
 Si activa esta casilla, al guardar los cambios, un cuadro de mensaje mostrará cualquier conflicto que se haya producido entre sus cambios y los realizados por otro usuario.  
  
 **Advertir sobre las tablas afectadas**  
 Presenta un cuando de diálogo de advertencia que muestra las tablas a las que va a afectar la acción y solicita confirmación.  
  
 **Impedir guardar cambios que requieran volver a crear tablas**  
 Evita que un usuario realice modificaciones que requieran volver a crear la tabla. Las acciones siguientes pueden requerir que se vuelva a crear una tabla:  
  
-   Agregar una nueva columna en la mitad de la tabla  
  
-   Quitar una columna  
  
-   Cambiar la nulabilidad de columnas  
  
-   Cambiar el orden de las columnas  
  
-   Cambiar el tipo de datos de una columna  
  
 **Vista de tabla predeterminada**  
 Seleccione la forma en que desea ver las tablas en los diseñadores:  
  
-   **Standard**  
  
     Muestra el encabezado de tablas, todos los nombres de columna, tipos de datos y la configuración Permitir valores NULL.  
  
-   **Nombres de columna**  
  
     Muestra los nombres de columna.  
  
-   **Key**  
  
     Muestra el encabezado de tabla y las columnas de clave principal.  
  
-   **Solo nombre**  
  
     Solo muestra el encabezado de tabla con su nombre.  
  
-   **Personalizado**  
  
     Permite elegir las columnas que se muestran.  
  
 **Iniciar cuadro de diálogo Agregar tabla en un nuevo diagrama**  
 Abre automáticamente el cuadro de diálogo **Agregar tabla** cuando se abren los diseñadores.  
  
  
