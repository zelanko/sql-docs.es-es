---
title: Nuevas características de interfaz gráfica de usuario de SSMA para MySQL (MySQLToSQL) | Documentos de Microsoft
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 0e59e2dc-1e4a-47c0-a5c3-ae7b5f5e469c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b9eb20c4a6a6eb789d7c37f02865fd4f2a7bd24c
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34776291"
---
# <a name="new-gui-features-in-ssma-for-mysql-mysqltosql"></a>Nuevas características de interfaz gráfica de usuario de SSMA para MySQL (MySQLToSQL)
Este capítulo describe nuevas características de interfaz de usuario de SSMA  
  
## <a name="layouts"></a>Diseños de  
Esta característica le permite elegir uno de dos ventanas predefinidos decoración o crear un diseño propio. Para obtener acceso a submenú de diseño, en el menú Ver, seleccione diseños. Puede elegir una de las plantillas existentes, agregar diseño actual o administrar los diseños.  
  
### <a name="add-current-layout"></a>Agregar diseño actual  
Para guardar el diseño actual de windows, en el menú Ver, seleccione diseños, a continuación, haga clic en Agregar diseño actual.  
  
### <a name="choose-predefined-layout"></a>Elegir el diseño predefinido  
Para elegir uno de los formatos predefinidos, en el menú Ver seleccione diseños, haga clic en diseño predeterminado o sin exploradores. También puede utilizar métodos abreviados de Ctrl + Alt + 1 o Ctrl + Alt + 2 diseños predefinidos respectivamente.  
  
### <a name="choose-user-defined-layout"></a>Elegir el diseño definido por el usuario  
Para elegir el diseño definido por el usuario, en el menú Ver seleccione diseños, haga clic en uno el diseño definido por el usuario. También puede usar los accesos directos definidos para los diseños.  
  
### <a name="manage-layouts"></a>Administrar los diseños  
Para abrir el cuadro de diálogo Administrar diseños, en el menú Ver, elija a los diseños y haga clic en administrar diseños. En el cuadro de diálogo Administrar diseños encontrará una lista de las plantillas existentes en el lado izquierdo del cuadro de diálogo. Puede seleccionar el diseño para cambiar su configuración. También puede cambiar el orden de los diseños de la lista o eliminar el diseño con botones en la parte superior de la lista. En el lado derecho del cuadro de diálogo puede cambiar la configuración de diseño siguientes:  
  
-   Nombre de diseño  
  
-   Sincronización de los exploradores de metadatos  
  
-   Visibilidad y el ancho de los exploradores de metadatos de origen y de destino  
  
-   Visibilidad de las ventanas de origen o destino y sus tamaños  
  
-   Visibilidad y el alto de ventanas auxiliares  
  
## <a name="bookmarks"></a>Marcadores  
Esta característica permite establecer uno o más marcadores en el origen o código de destino, rápido se encuentra un marcador mediante los métodos abreviados, administrar los marcadores con un cuadro de diálogo descriptivo.  
  
### <a name="toggle-bookmark"></a>Alternar marcador  
Se puede establecer/anular un marcador de las maneras siguientes:  
  
-   Use el botón Alternar marcador encima de la ventana SQL de origen o destino  
  
-   Haga clic en el área gris de la izquierda de la ventana SQL  
  
-   Utilice Ctrl + Mayús +&lt;0..9&gt; para establecer el marcador numerado  
  
### <a name="bookmark-navigation"></a>Navegación de marcador  
Puede realizar a través de los marcadores de las maneras siguientes:  
  
-   Usar botones siguiente marcador marcador anterior en la parte superior de la ventana SQL  
  
-   Utilice Ctrl +&lt;0..9&gt; para encontrar marcador numerado  
  
-   Utilice los botones Ir a o ver código fuente en el cuadro de diálogo de administrar marcadores  
  
### <a name="removing-bookmark"></a>Quitar marcador  
Puede quitar un marcador de las maneras siguientes:  
  
-   Use el botón Borrar en la parte superior de la ventana SQL para quitar todos los marcadores del documento actual  
  
-   Usar botones quitar o quitar todo en el cuadro de diálogo de administrar marcadores  
  
### <a name="manage-bookmarks"></a>Administrar marcadores  
Para abrir el cuadro de diálogo Administrar marcadores, en el menú Edición, haga clic en Administrar marcadores. En el cuadro de diálogo verá una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.  
  
## <a name="object-history"></a>Historial de objetos  
Historial de objetos de interfaz gráfica de usuario permite las siguientes ventajas al navegar objetos:  
  
-   Puede usar los botones Atrás y hacia delante para navegar por los objetos que ya ha visitado  
  
-   Cuando copia en el objeto, hace una copia en la misma ficha que han dejado  
  
-   Cuando se vuelve a la pestaña y el objeto es SQL, hace una copia en la misma posición del cursor que han dejado  
  
## <a name="advanced-search-capabilities"></a>Capacidades de búsqueda avanzada  
Capacidades de búsqueda avanzada proporcionan las características de búsqueda eficaces y flexibles y permiten encontrar la declaración del objeto, obtener información sobre los objetos, realizar la búsqueda rápida, realizar buscando en categorías mediante patrones etcetera avanzada de objetos.  
  
### <a name="get-quick-information"></a>Obtener información rápida  
Puede obtener información rápida sobre el objeto en la posición del cursor de las maneras siguientes:  
  
-   Haga clic en el botón información rápida en la parte superior de la ventana de SQL  
  
-   Seleccione la información rápida en el menú emergente de menú contextual  
  
-   Presione Ctrl + Mayús + barra espaciadora  
  
### <a name="find-declaration"></a>Busque la declaración  
Puede ir a la declaración del objeto en la posición del cursor de las maneras siguientes:  
  
-   Haga clic en el botón Ir a declaración encima de la ventana SQL  
  
-   Seleccione ir a declaración en el menú emergente de menú contextual  
  
-   Presione F12  
  
### <a name="quick-search"></a>Búsqueda rápida  
Puede realizar búsquedas de texto rápidas con las siguientes características:  
  
-   Puede empezar a buscar mediante el uso de método abreviado Ctrl + F  
  
-   Puede repetir la última búsqueda hacia delante mediante el uso de F3  
  
-   Se puede repetir la última búsqueda hacia atrás mediante el uso de MAYÚS + F3  
  
-   Puede buscar siguiente repetición de la palabra en la posición del cursor mediante Ctrl + F3  
  
-   Puede buscar la repetición anterior de la palabra en la posición del cursor mediante Ctrl + Mayús + F3  
  
-   También puede realizar todas estas acciones con elementos de menú.  
  
### <a name="advanced-search"></a>Búsqueda avanzada  
Para abrir el cuadro de diálogo de búsqueda avanzada, en la búsqueda de punto del menú Edición, a continuación, haga clic en búsqueda avanzada. En el cuadro de diálogo podrá buscar cualquier objeto con el patrón. En la parte superior del cuadro de diálogo puede elegir categorías de área y el objeto de búsqueda.  
  
