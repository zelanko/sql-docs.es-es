---
title: Página elementos dependientes (Administrador de informes) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4dcfb311-e9c3-4c5d-b2e0-018d79f37d2e
caps.latest.revision: 29
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: 0496334695c72a78afe3fedb87763cfaacd66e35
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108050"
---
# <a name="dependent-items-page-report-manager"></a>Página de elementos dependientes (Administrador de informes)
  Use la página Elementos dependientes para ver una lista de informes y modelos que hacen referencia a un origen de datos compartido. El icono de cada tipo de elemento indica si se trata de un informe o de un modelo. Esta página puede mostrarse en la vista de lista o en la vista Detalles. Use la vista Detalles para mostrar más información sobre cada elemento. Esta vista también incluye opciones de página adicionales. Para ayudarle a administrar el origen de datos compartido, esta página proporciona vínculos a los informes y modelos que usan el origen de datos, las métricas sobre cuándo se ejecutó o modificó el informe o el modelo por última vez, y los botones Eliminar y Mover de manera que pueda quitar los informes y modelos con facilidad que ya no se usan, o moverlos a una ubicación diferente mientras determina si todavía son necesarios.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-dependent-items-page"></a>Para abrir la página Elementos dependientes  
  
1.  Abra el Administrador de informes y busque el origen de datos compartido del que desea ver los elementos dependientes.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Esto abre la página de propiedades General del origen de datos.  
  
4.  Seleccione la pestaña **Elementos dependientes** .  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Muestra el nombre del informe o del modelo. Haga clic en el nombre del informe para abrirlo. Haga clic en el nombre del modelo para abrir sus páginas de propiedades.  
  
 **Descripción**  
 Muestra la descripción del informe o del modelo.  
  
 **Eliminar**  
 Haga clic para eliminar el informe o el modelo de la base de datos del servidor de informes. Antes de hacer clic en **Eliminar**, active la casilla situada junto a cada elemento que desee eliminar.  
  
 **Mover**  
 Haga clic para cambiar de posición un informe o un modelo dentro de la jerarquía de carpetas. Antes de hacer clic en **Mover**, active la casilla situada junto a cada elemento que desee mover. Al hacerlo, se abre la página para mover elementos, en la que puede examinar las carpetas para seleccionar una nueva ubicación.  
  
 **Editar**  
 Haga clic en el icono de propiedades para obtener acceso a las páginas de propiedades de un informe o un modelo.  
  
 **Tipo**  
 Muestra el icono del tipo de elemento.  
  
 **Fecha de modificación**  
 Muestra la fecha y la hora en que se modificó el informe o el modelo por última vez.  
  
 **Modificado por**  
 Muestra el nombre del usuario que modificó las propiedades del elemento por última vez.  
  
 **Cuando se ejecuta**  
 Para los informes que se ejecutan como instantáneas de ejecución de informes, muestra la fecha y la hora en que se actualizó el informe por última vez.  
  
## <a name="see-also"></a>Vea también  
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [El Administrador de informes &#40;modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [El contenido de página &#40;el Administrador de informes&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  