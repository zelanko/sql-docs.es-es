---
title: Página de propiedades generales, carpetas (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 31d99d9b-2303-4bae-9466-fb67b97cf11a
caps.latest.revision: 25
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4ee15c703cab10ced93359c91f170e7de0768e3d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37255827"
---
# <a name="general-properties-page-folders-report-manager"></a>Página de propiedades generales, carpetas (Administrador de informes)
  Use la página de propiedades General de carpetas para ver y establecer las propiedades de las carpetas que cree. En la parte superior de la página, aparece información sobre quién creó o modificó la carpeta y cuándo se modificó en la página Propiedades generales.  
  
 Las propiedades de carpeta también incluyen opciones de seguridad. Para obtener más información acerca de la seguridad de carpeta, consulte [proteger carpetas](security/secure-folders.md).  
  
 Las carpetas que tienen una finalidad específica, como Inicio, Mis informes y Carpetas de usuarios, no se pueden mover en el espacio de nombres del servidor de informes y su nombre no puede cambiarse. La página de propiedades General no está disponible para estas carpetas.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-general-properties-page-for-a-folder"></a>Para abrir la página de propiedades General de una carpeta  
  
1.  Abra el Administrador de informes y abra la carpeta para la que desea ver o configurar las propiedades.  
  
2.  En el título de la carpeta, en la barra de herramientas, haga clic en **Configuración de carpeta**.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Especifique un nombre para la carpeta. El nombre debe incluir al menos un carácter alfanumérico. También puede incluir espacios y algunos símbolos. No use los caracteres ; ? : @ & = +, $ * \< > | "o / al especificar un nombre.  
  
 **Descripción**  
 Escriba una descripción del contenido de la carpeta. Esta descripción se mostrará en la página Contenido para los usuarios que tengan permisos de acceso a la carpeta.  
  
 **Ocultar en la vista de lista**  
 Seleccione esta opción para ocultar la carpeta a usuarios que usen el modo de vista de lista en el Administrador de informes. El modo de vista de lista es el formato de vista predeterminado al explorar la jerarquía de carpetas del servidor de informes. En la vista de lista, los nombres y descripciones de elementos se presentan en formato horizontal. El formato alternativo es la vista Detalles. La vista Detalles no incluye descripciones, pero sí otra información acerca del elemento. Aunque se puede ocultar un elemento en la vista de lista, no se puede ocultar en la vista Detalles. Si desea restringir el acceso a un elemento, deberá crear una asignación de roles.  
  
 **Aplicar**  
 Haga clic para guardar los cambios.  
  
 **Eliminar**  
 Haga clic para quitar la carpeta y su contenido.  
  
 **Mover**  
 Haga clic para cambiar de posición un informe o una carpeta dentro del espacio de nombres del servidor de informes. Al hacer clic en este botón, se abre la página Mover elementos, que permite buscar una nueva ubicación de carpeta.  
  
## <a name="see-also"></a>Vea también  
 [El Administrador de informes &#40;modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
