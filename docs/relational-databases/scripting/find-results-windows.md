---
title: Ventanas Resultados de la búsqueda | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssms-scripting
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.findresults1
- findresultswindow
- vs.findresults2
helpviewer_keywords:
- Find Results Windows dialog box
ms.assetid: 3b68dbb7-26d6-4bc9-bd2c-c27e5dc385c3
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6458a5d2c9924cb77e72fe46ca5f17ad8d8ce1fc
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="find-results-windows"></a>Ventanas Resultados de la búsqueda
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  Las dos ventanas Resultados de la búsqueda muestran las coincidencias encontradas utilizando las pestañas **Buscar en archivos** o **Reemplazar en archivos** del cuadro de diálogo **Buscar y reemplazar** . El comando **Opciones de resultados** de **Buscar en archivos** y **Reemplazar en archivos** le permite elegir la ventana Resultados de la búsqueda donde desea que se muestren todas las coincidencias encontradas.  
  
 La ventana Resultados de la búsqueda seleccionada se abrirá automáticamente cada vez que se encuentren coincidencias. Para mostrar la ventana Resultados de la búsqueda de forma manual, haga clic en **Otras ventanas** en el menú **Ver** y, a continuación, haga clic en **Resultados de la búsqueda 1** o **Resultados de la búsqueda 2**.  
  
 Para que se muestre el archivo de código y saltar a la línea donde se ha producido una coincidencia, haga doble clic en cualquier línea de la lista de resultados. El archivo de origen se mostrará en el Editor de código con el punto de inserción situado en el lugar donde comience el texto coincidente. Aparecerá un símbolo en el margen del indicador del editor para marcar la línea que incluye la coincidencia y, en la barra de estado, se mostrará su texto completo.  
  
## <a name="toolbar-buttons"></a>Botones de la barra de herramientas  
 Los botones de la barra de herramientas que se muestran a continuación le ayudarán a recorrer la lista de resultados y saltar a las líneas del código donde se hayan encontrado coincidencias.  
  
 **marca de página + flecha arriba**  
 Se desplaza a la línea donde se ha encontrado la coincidencia seleccionada.  
  
 **página + flecha izquierda**  
 Se desplaza a la línea de la coincidencia anterior.  
  
 **página + flecha derecha**  
 Se desplaza a la línea de la siguiente coincidencia.  
  
 **Borrar todo**  
 Quita todas las coincidencias de la lista **Resultados** .  
  
## <a name="shortcut-keys"></a>Teclas de acceso directo  
 Las teclas de acceso directo que se muestran a continuación le ayudarán a navegar rápidamente por las coincidencias encontradas.  
  
 CTRL+INICIO  
 Se desplaza a la parte superior de la ventana Resultados de la búsqueda.  
  
 CTRL+FIN  
 Se desplaza a la parte inferior de la ventana Resultados de la búsqueda.  
  
 RE PÁG  
 Se desplaza hacia arriba, hasta el siguiente grupo de coincidencias.  
  
 AV PÁG  
 Se desplaza hacia abajo, hasta el siguiente grupo de coincidencias.  
  
 FLECHA ARRIBA  
 Selecciona la coincidencia anterior.  
  
 FLECHA ABAJO  
 Selecciona la siguiente coincidencia.  
  
## <a name="search-result-entries"></a>Buscar entradas de resultados  
 Las entradas de la lista de resultados proporcionan la siguiente información:  
  
-   Ruta de acceso completa  
  
-   Nombre de archivo  
  
-   Número de línea  
  
-   Texto completo de la línea que contiene la coincidencia  
  
> [!TIP]  
>  Puede utilizar **Búsqueda rápida** para recorrer una lista de resultados extensa. Abra y acople la ventana Resultados de la búsqueda y, a continuación, haga clic en el botón triangular **Ver** en la pestaña **Buscar** y cambie a **Búsqueda rápida**. Establezca el campo **Buscar en** de la búsqueda en **Ventana activa**, escriba una cadena **Buscar** y, a continuación, haga clic en **Buscar siguiente**. Esto le permitirá recorrer la lista de resultados para buscar coincidencias encontradas en carpetas o archivos específicos, o bien buscar coincidencias en líneas de código donde aparezcan también otros términos clave.  
  
## <a name="summary-lines"></a>Líneas de resumen  
 Cada conjunto de resultados de la búsqueda comienza con una línea que indica los parámetros de búsqueda y termina con una línea de estadísticas. Por ejemplo, la lista de resultados de una búsqueda **Buscar en archivos** en todos los documentos abiertos para encontrar cadenas que coincidan con la expresión regular "`var[1-3]&par`" debería comenzar con esta línea de parámetros de búsqueda:  
  
 `Find all "var[1-3]&par" Regular Expression, All Open Documents`  
  
 y debería concluir con esta línea de estadísticas:  
  
 `Total found: 57  Matching files: 23  Total files searched: 59`  
  
 La lista de resultados de una búsqueda **Reemplazar en archivos** en todos los documentos abiertos para reemplazar cadenas que coincidan con la expresión regular "`var[1-3]&par`" con la cadena "`sample`" debería comenzar con esta línea de parámetros de búsqueda:  
  
 `Replace "var[1-3]&par", "sample", Regular Expression, All Open Documents`  
  
 y debería concluir con esta línea de estadísticas:  
  
 `Total replaced: 57  Matching files: 23  Total files searched: 59`  
  
  
