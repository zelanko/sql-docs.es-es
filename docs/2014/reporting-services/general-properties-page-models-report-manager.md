---
title: Página de propiedades generales, modelos (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.modelproperties.general.f1
ms.assetid: 7ad59850-8135-4c4d-95e9-6d705b6d77a8
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 052ea58263c2167035f09d7c81c0e1732c530e03
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082727"
---
# <a name="general-properties-page-models-report-manager"></a>Página Propiedades generales, Modelos (Administrador de informes)
  Use la página Propiedades generales para los modelos de informes con el fin de cambiar el nombre, eliminar, mover o reemplazar el archivo de definición de modelo (.smdl). En la parte superior de la página, se incluye información detallada de quién creó o modificó el modelo, y cuándo tuvieron lugar los cambios.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-general-properties-page-for-a-model"></a>Para abrir la página propiedades General de un modelo  
  
1.  Abra el Administrador de informes y busque el modelo del que desea ver o configurar las propiedades.  
  
2.  Mantenga el mouse sobre el modelo y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página Propiedades generales correspondiente al modelo.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifica el nombre del modelo. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios y algunos símbolos. No utilice los caracteres siguientes al especificar un nombre:  
  
 ; ? : \@ & = +, $ / * \< > | " /  
  
 **Descripción**  
 Escriba una descripción del modelo. Esta descripción se mostrará en la página Contenido a los usuarios que tengan permiso de acceso al modelo.  
  
 **Oculto en la vista de lista**  
 Active esta casilla para ocultar el elemento cuando la carpeta se establece en la vista de lista. La vista de lista es un modo de visualización del contenido de la carpeta compatible con el Administrador de informes. Puede establecer esta opción [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para definir cómo este elemento se ve en el Administrador de informes. Para obtener más información acerca de los modos de vista en el Administrador de informes, vea [página contenido &#40;el Administrador de informes&#41;](../../2014/reporting-services/contents-page-report-manager.md).  
  
 **Aplicar**  
 Haga clic para guardar los cambios.  
  
 **Eliminar**  
 Haga clic para quitar el modelo de la base de datos del servidor de informes. Al eliminar un modelo, no se elimina el origen de datos compartido dependiente que proporciona información de conexión, ni se eliminan informes que usan el modelo como un origen de datos. Sin embargo, una vez eliminado el modelo, ya no se ejecutarán los informes que usan el modelo.  
  
 **Mover**  
 Haga clic para cambiar la posición de un modelo en la jerarquía de carpetas del servidor de informes. Si hace clic en este botón, se abre la página Mover elementos, en la que puede examinar las carpetas para buscar una nueva ubicación de carpeta. Para obtener más información, consulte [página Mover elementos &#40;el Administrador de informes&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Guardar**  
 Haga clic para guardar una copia de solo lectura de la definición del modelo. En función de las asociaciones de archivos definidas en su equipo, el archivo se abrirá en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o en otra aplicación. En la mayoría de los casos, el modelo se abre como un archivo XML.  
  
 La copia que se abre es idéntica a la definición de modelo original publicada inicialmente en el servidor de informes. Las propiedades del modelo establecidas después de publicarlo, como las propiedades del origen de datos, no se reflejan en el informe que se abre.  
  
 Puede modificar la definición del modelo y guardarla como un archivo nuevo en una carpeta compartida, y cargar la definición del modelo en el servidor de informes como un nuevo elemento. Las modificaciones que realice en la definición del modelo mientras está abierto en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (u otra aplicación) no se guardan directamente en el servidor de informes. Deberá cargar el archivo para publicar el modelo modificado en el servidor de informes.  
  
 Tenga en cuenta que si desea abrir el modelo de informe en el Diseñador de modelos, debería guardar el modelo como archivo .smdl y, a continuación, agregar el archivo .smdl a un proyecto en el Diseñador de modelos.  
  
 **Reemplazar**  
 Haga clic para reemplazar la definición de modelo por otra diferente de un archivo .smdl que se encuentra en el sistema de archivos. Si actualiza una definición de modelo, debe restablecer la configuración del origen de datos compartido cuando la actualización haya finalizado.  
  
 **Regenerar el modelo**  
 Haga clic para regenerar un modelo predeterminado que reemplaza la versión actual. Esta opción aparece una vez se ha generado el modelo. El modelo generado se basa en el origen de datos compartido. No se puede personalizar antes de generarse. Sin embargo, después de generarlo, puede hacer clic en **Editar** para abrir la definición de modelo, guardarlo en el sistema de archivos y, a continuación, agregarla a un proyecto en el Diseñador de modelos. Después de precisar el modelo, puede cargarlo en el servidor de informes como un nuevo elemento o hacer clic en **Actualizar** en esta página para reemplazar el modelo generado por la versión revisada en el Diseñador de modelos.  
  
## <a name="see-also"></a>Vea también  
 [Enlazar un informe o modelo a un origen de datos compartido &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Servidor de informes en Management Studio (Ayuda F1)](tools/report-server-in-management-studio-f1-help.md)  
  
  
