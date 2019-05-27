---
title: Administración de marcadores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [SQL Server Management Studio]
ms.assetid: 67cc3fd6-3238-4c58-a3ec-2d3b0438143a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6741660b7b7985356c59ffe47b53c376a55338e4
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66063909"
---
# <a name="manage-bookmarks"></a>Administrar marcadores
  Cuando trabaja en un editor de código, la ventana **Marcadores** permite crear vínculos a líneas específicas de código en el documento. Puede abrir esta ventana desde el menú **Ver** .  
  
 Para crear y navegar a través de los marcadores, haga clic en los botones que se ubican en la barra de herramientas del **Editor de texto** y en la parte superior de la ventana **Marcadores** . Puede agregar y quitar marcadores, activarlos o deshabilitarlos, y organizarlos en carpetas. También están disponibles algunos comandos desde el menú contextual de la ventana **Marcadores** . Para agregar o quitar un marcador, coloque el punto de inserción en la línea deseada del editor y haga clic en **Cambiar a un marcador de la línea actual**. Para activar un marcador, active su casilla en la ventana **Marcadores** ; para deshabilitarlo (pero no quitarlo), desactive la casilla.  
  
## <a name="text-editor-toolbar"></a>Barra de herramientas del Editor de texto  
 Cuando un documento se abre en el editor, se habilitan los siguientes botones en la barra de herramientas del **Editor de texto** . Para mostrar la barra de herramientas del Editor de texto cuando se encuentra en el **Editor de consultas** , seleccione **Barras de herramientas** en el menú **Ver**y luego haga clic en **Editor de texto**.  
  
 **Cambiar a un marcador de la línea actual**  
 Agrega o elimina un marcador en la línea seleccionada del documento en el editor activo. No modifica la línea de código marcada.  
  
 **Mover el carácter de intercalación al marcador anterior**  
 Selecciona el marcador anterior que se encuentra habilitado en la ventana **Marcadores** . Cuando se llega al primer marcador, se desplazará hasta el último. Cuado sea necesario, abra el archivo donde se encuentre el marcador seleccionado en el editor. Desplace el documento hasta la línea marcada y coloque allí el punto de inserción.  
  
 **Mover el carácter de intercalación al siguiente marcador**  
 Selecciona el marcador siguiente que se encuentra habilitado en la ventana **Marcadores** . Cuando se llega al último marcador, se desplazará hasta el primero. Cuado sea necesario, abra el archivo donde se encuentre el marcador seleccionado en el editor. Desplace el documento hasta la línea marcada y coloque allí el punto de inserción.  
  
 **Borrar todos los marcadores del documento actual**  
 Muestra un mensaje de confirmación y luego elimina todos los marcadores del documento activo. No elimina las líneas de código que se marcaron.  
  
> [!CAUTION]  
>  No es posible deshacer este procedimiento. Posteriormente, puede usar **Cambiar a un marcador de la línea actual** para crear nuevos marcadores. Para deshabilitar los marcadores, pero no eliminarlos, desactive las casillas de la ventana **Marcadores** .  
  
## <a name="bookmarks-window"></a>Ventana Marcadores  
 Para organizar los marcadores, cree carpetas de marcadores en la ventana **Marcadores** . Arrastre y coloque los marcadores en las carpetas. Los siguientes botones están disponibles en la parte superior de la ventana **Marcadores** .  
  
 **Cambiar a un marcador de la línea actual.**  
 Agrega o elimina un marcador en la línea seleccionada del documento en el editor activo. No modifica la línea de código marcada.  
  
 **Nueva carpeta**  
 Agrega una carpeta a la ventana **Marcadores** .  
  
> [!TIP]  
>  En una extenso archivo de código, resulta útil organizar los marcadores en carpetas relacionadas con las tareas. Al seleccionar una carpeta se habilitan los botones **Marcador anterior en carpeta** y **Marcador siguiente en carpeta** .  
  
 **Mover el carácter de intercalación al marcador anterior**  
 Selecciona el marcador anterior que se encuentra habilitado en la ventana **Marcadores** . Cuando se llega al primer marcador, se desplazará hasta el último. Cuado sea necesario, abra el archivo donde se encuentre el marcador seleccionado en el editor. Desplace el documento hasta la línea marcada y coloque allí el punto de inserción.  
  
 **Mover el carácter de intercalación al siguiente marcador**  
 Selecciona el marcador siguiente que se encuentra habilitado en la ventana **Marcadores** . Cuando se llega al último marcador, se desplazará hasta el primero. Cuado sea necesario, abra el archivo donde se encuentre el marcador seleccionado en el editor. Desplace el documento hasta la línea marcada y coloque allí el punto de inserción.  
  
 **Mover el carácter de intercalación al marcador anterior de la carpeta actual**  
 Selecciona el marcador anterior que se encuentra habilitado en la misma carpeta de la ventana **Marcadores** . Cuando se llega al primer marcador, se desplazará hasta el último de esa carpeta. Cuado sea necesario, abra el archivo donde se encuentre el marcador seleccionado en el editor. Desplace el documento hasta la línea marcada y coloque allí el punto de inserción.  
  
 **Mover el carácter de intercalación al siguiente marcador de la carpeta actual**  
 Selecciona el siguiente marcador que se encuentra habilitado en la misma carpeta de la ventana **Marcadores** . Cuando se llega al último marcador, se desplazará hasta el primero de esa carpeta. Cuado sea necesario, abra el archivo donde se encuentre el marcador seleccionado en el editor. Desplace el documento hasta la línea marcada y coloque allí el punto de inserción.  
  
 **Deshabilitar/Habilitar todos los marcadores**  
 Activa o desactiva las casillas de todos los marcadores de la ventana **Marcadores** . No elimina los marcadores ni modifica las líneas de código marcadas.  
  
 **Eliminar**  
 Quita el marcador seleccionado de la ventana **Marcadores** y del documento donde se encuentra el marcador. No quita la línea de código que se marcó.  
  
 Casillas de marcador  
 Cada marcador tiene su propia casilla. Para activar un marcador existente, active su casilla en la ventana **Marcadores** . Para ocultar (pero no eliminar) un marcador existente, desactive su casilla en la ventana **Marcadores** .  
  
## <a name="bookmarks-window-shortcut-menu"></a>Menú contextual de la ventana Marcadores  
 Cuando se hace clic con el botón derecho en una entrada de la ventana **Marcadores** , están disponibles los siguientes comandos en el menú contextual.  
  
 **Eliminar**  
 Quita el marcador seleccionado de la ventana **Marcadores** y del documento donde se encuentra el marcador. No quita la línea de código que se marcó.  
  
 **Cambiar el nombre**  
 Permite asignar un nuevo nombre para mostrar a una carpeta de marcadores.  
  
 **Deshabilitar/Habilitar marcador**  
 Activa o desactiva la casilla del marcador seleccionado de la ventana **Marcadores** . No elimina el marcador ni modifica la línea de código marcada.  
  
 **Deshabilitar/Habilitar todos los marcadores**  
 Activa o desactiva las casillas de todos los marcadores de la ventana **Marcadores** . No elimina los marcadores ni modifica las líneas de código marcadas.  
  
## <a name="see-also"></a>Vea también  
 [Métodos abreviados de teclado de SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
