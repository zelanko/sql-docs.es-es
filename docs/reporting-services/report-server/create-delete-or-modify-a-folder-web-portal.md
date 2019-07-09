---
title: Crear, eliminar o modificar una carpeta - Reporting Services | Microsoft Docs
ms.date: 06/26/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 70a38879-856c-414b-8479-5f9dead38f15
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 874fb7ba143c8f08a0f25501e1852b4d2b280cb2
ms.sourcegitcommit: c0e48b643385ce19c65ca6e348ce83b2d22b6514
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2019
ms.locfileid: "67492853"
---
# <a name="create-delete-or-modify-a-folder---reporting-services"></a>Crear, eliminar o modificar una carpeta - Reporting Services
  Puede crear carpetas para organizar y administrar los elementos que publica en un servidor de informes. La creación de carpetas puede ayudar a los usuarios a buscar informes de su interés. Para administradores de contenido, las carpetas proporcionan un marco para aplicar permisos. Puede crear asignaciones de roles en carpetas concretas para restringir el acceso a los informes que se están desarrollando o que no se deberían distribuir de manera amplia.  

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

## <a name="to-create-a-folder"></a>Para crear una carpeta  
  
1.  Inicie el [Administrador de informes &#40;Modo nativo de SSRS&#41;](https://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  En el Administrador de informes, seleccione la carpeta Inicio y haga clic en **Nueva carpeta**. O bien, para crear una carpeta en una carpeta existente, navegue hasta dicha carpeta en la página **Contenido** y haga clic en ella para abrirla. A continuación, haga clic en **Nueva carpeta**.  
  
     Se abre la página **Nueva carpeta** .  
  
3.  Escriba el nombre de la carpeta. Puede incluir espacios, pero no caracteres reservados que se utilicen para la codificación de direcciones URL: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. No se puede escribir una serie de nombres de carpetas para crear varias carpetas al mismo tiempo.  
  
4.  Si lo desea, escriba una descripción.  
  
5.  Seleccione **Ocultar en la vista de lista** si no desea mostrar la carpeta en la vista predeterminada de la página **Contenido** . La carpeta estará visible para los usuarios solo cuando hagan clic en **Mostrar detalles** en la página **Contenido** .  
  
6.  Haga clic en **Aceptar**.  
  
## <a name="to-delete-a-folder"></a>Para eliminar una carpeta  
  
1.  En el Administrador de informes, navegue a la página **Contenido** y localice el elemento que desee modificar.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Eliminar**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="to-modify-or-delete-a-folder"></a>Para modificar o eliminar una carpeta  
  
1.  En el Administrador de informes, navegue a la página **Contenido** y localice el elemento que desee modificar.  
  
2.  Mantenga el mouse sobre el elemento y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abre la página de propiedades General.  
  
4.  Para cambiar la ubicación de la carpeta, haga clic en **Mover**. Escriba la ubicación de la carpeta de destino o elija la carpeta de destino desde el árbol y, a continuación, haga clic en **Aceptar**.  
  
5.  O bien, modifique las propiedades de la carpeta de las siguientes maneras:  
  
    -   Para modificar el texto que se muestra sobre la carpeta, escriba un nombre o una descripción.  
  
    -   Para mostrar la carpeta en la vista predeterminada en la página **Contenido** , desactive **Ocultar en la vista de lista**.  
  
6.  O bien, haga clic en **Eliminar**para quitar la carpeta y su contenido.  
  
7.  Haga clic en **Aplicar** para guardar los cambios.  

::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
 
## <a name="to-create-a-folder"></a>Para crear una carpeta  
  
1. Abra [el portal web de un servidor de informes (modo nativo de SSRS)](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
2. Navegue hasta la carpeta o subcarpeta donde desea ubicar la nueva carpeta. Seleccione el **inicio** carpeta seleccionando el **examinar** en la barra de herramientas en la parte superior izquierda de la página para crearlo en la parte superior de la jerarquía de carpetas.  
  
3. Seleccione el **New** botón en la parte superior derecha de la barra de herramientas del servidor de informes y, a continuación, seleccione **carpeta** en el menú desplegable.  
  
4. En el **cree una nueva carpeta (nombre de la carpeta actual)** diálogo cuadro, escriba el nombre de la nueva carpeta que se va a crear. Puede incluir espacios, pero no caracteres reservados que se utilicen para la codificación de direcciones URL: \; \? \: \@ \& \= \+ \, \$ \/ \* \< \> \|. Tampoco se puede escribir una serie de nombres de carpetas para crear varias carpetas al mismo tiempo.  
  
5. Seleccione **crear** para completar la acción.  
  
## <a name="to-delete-a-folder"></a>Para eliminar una carpeta  
  
1. En el portal web, vaya a la jerarquía de carpetas y busque la carpeta que desea eliminar.  
  
2. El derecho click carpeta y seleccione **eliminar** en el menú desplegable.  
  
3. Seleccione el **eliminar** situado en la **eliminar <foldername>**  cuadro de diálogo para confirmar la eliminación.  
  
## <a name="to-modify-a-folders-properties"></a>Para modificar las propiedades de una carpeta  
  
1. En el portal web, vaya a la jerarquía de carpetas y busque la carpeta que desea eliminar.  
  
2. El derecho click carpeta y seleccione **eliminar** en el menú desplegable.  
  
3. Seleccione la pestaña **Propiedades**. El **propiedades** página se muestra de forma predeterminada.  
  
4. Puede cambiar el nombre de la carpeta en la *nombre** cuadro de texto.  
  
5. Puede agregar o cambiar la descripción de la carpeta en la *descripción** cuadro de texto.  
  
6. Puede ocultar o mostrar la carpeta activando o desactivando la **ocultar este elemento** casilla de verificación, respectivamente.  
  
7. Seleccione **aplicar** para guardar los cambios de propiedades.  
  
8. Si lo desea, puede mover o eliminar la carpeta seleccionando el **mover** o **eliminar** botones en la parte superior de la **propiedades** página. Consulte la [mover o eliminar un elemento (portal web)](../../reporting-services/report-server/move-or-delete-an-item-report-manager.md) artículo para obtener más información.  
  
## <a name="see-also"></a>Vea también  
 [Creación, eliminación o modificación de una carpeta (portal web)](../../reporting-services/report-server/create-delete-or-modify-a-folder-web-portal.md)   
 [Administración de contenido del servidor de informes (modo nativo de SSRS)](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)    
  
::: moniker-end