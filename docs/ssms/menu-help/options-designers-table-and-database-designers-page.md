---
title: "Opciones (Diseñadores - página Diseñadores de tablas y bases de datos) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Designers.Table_Designer
ms.assetid: b43f4b97-17b9-4004-a824-f77b9e145741
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 79e728f7cf2c300338e202b3e9cae27226f70a50
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="options-designers---table-and-database-designers-page"></a>Opciones (Diseñadores - Página Diseñadores de tablas y bases de datos)
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
  

