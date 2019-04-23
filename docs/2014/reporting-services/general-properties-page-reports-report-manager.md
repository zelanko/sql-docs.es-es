---
title: Página Propiedades generales, informes (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 66c99d28-ab41-45f0-bf02-ed560293595d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c44bc306aaa1e55aa5005663ecfcfbf261576593
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59940307"
---
# <a name="general-properties-page-reports-report-manager"></a>Página d propiedades generales, informes (Administrador de informes)
  Use la página de propiedades General de informes para cambiar de nombre, eliminar, mover o reemplazar una definición de informe. Esta página se puede utilizar también para crear un informe vinculado. En la parte superior de la página, se incluye información detallada sobre quién creó o modificó el informe, y cuándo tuvieron lugar los cambios.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-general-properties-page-for-a-report"></a>Para abrir la página Propiedades generales de un informe  
  
1.  Abra el Administrador de informes y busque el informe del que desea ver o configurar las propiedades.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Especifique un nombre para el informe. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios en blanco y algunos símbolos. No use los caracteres ; ? : \@ & = + , $ * \< >  
  
 " o / al especificar el nombre.  
  
 **Descripción**  
 Escriba una descripción del informe. Esta descripción se mostrará en la página Contenido a los usuarios que tengan permisos de acceso al informe.  
  
 **Ocultar en la vista de lista**  
 Seleccione esta opción para ocultar el informe a usuarios que usen el modo de vista de lista en el Administrador de informes. El modo de vista de lista es el formato de vista predeterminado al explorar la jerarquía de carpetas del servidor de informes. En la vista de lista, los nombres y descripciones de elementos se presentan en formato horizontal. El formato alternativo es la vista Detalles. La vista Detalles no incluye descripciones, pero sí otra información acerca del elemento. Aunque se puede ocultar un elemento en la vista de lista, no se puede ocultar en la vista Detalles. Si desea restringir el acceso a un elemento, deberá crear una asignación de roles.  
  
 **Aplicar**  
 Haga clic para guardar los cambios.  
  
 **Eliminar**  
 Haga clic para quitar el informe de la base de datos del servidor de informes. Al eliminar un informe, se eliminan el historial de informe asociado y todas las suscripciones y programaciones específicas del informe. Si el informe está asociado a informes vinculados, éstos quedan invalidados.  
  
 **Mover**  
 Haga clic para cambiar la posición de un informe en la jerarquía de carpetas del servidor de informes. Si hace clic en este botón, se abre la página Mover elementos, en la que puede examinar las carpetas para buscar una nueva ubicación de carpeta. Para obtener más información, consulte [página Mover elementos &#40;el Administrador de informes&#41;](../../2014/reporting-services/move-items-page-report-manager.md).  
  
 **Crear informe vinculado**  
 Haga clic para abrir la página Nuevo informe vinculado. Para obtener más información acerca de esta página e informes vinculados, vea [página nuevo informe vinculado &#40;el Administrador de informes&#41;](../../2014/reporting-services/new-linked-report-page-report-manager.md).  
  
 **Guardar**  
 Haga clic para extraer una copia de solo lectura de la definición de informe. En función de las asociaciones de archivos definidas en su equipo, el archivo se abrirá en [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] o en otra aplicación. En la mayoría de los casos, el informe se abre como un archivo XML.  
  
 La copia que se abre es idéntica a la definición de informe original publicada inicialmente en el servidor de informes. Las propiedades del informe establecidas después de publicarlo, como los parámetros y las propiedades del origen de datos, no se reflejan en el informe que se abre.  
  
 Puede modificar la definición del informe y guardarla como un archivo nuevo en una carpeta compartida, y cargar la definición del informe en el servidor de informes como un nuevo elemento. Las modificaciones que realice en la definición de informe desde [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] (o desde otra aplicación) no se guardan directamente en el servidor de informes. Deberá cargar el archivo para publicar el informe modificado en el servidor de informes.  
  
 **Reemplazar**  
 Haga clic para reemplazar la definición de informe que se usa en el informe actual por una distinta obtenida del archivo .rdl ubicado en el sistema de archivos. Si actualiza una definición de informe, debe restablecer la configuración del origen de datos cuando la actualización haya finalizado.  
  
 **Cambiar vínculo**  
 Haga clic para seleccionar una definición de informe diferente para el informe vinculado. Esta opción aparece si el informe es un informe vinculado. Si el informe es vinculado, puede establecer esta propiedad de manera que reemplace la definición de informe.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
