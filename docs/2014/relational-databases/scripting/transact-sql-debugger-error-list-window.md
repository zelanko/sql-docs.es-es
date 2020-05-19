---
title: Ventana de lista de errores
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- error list window
- SQL Server Management Studio [SQL Server], error list window
ms.assetid: fae6327d-e268-44ae-a474-4a8f8f843129
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c88fb6beda0bef5a9e3d1980c1ffa78ed4944b70
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718410"
---
# <a name="error-list-window-management-studio"></a>Ventana Lista de errores (Management Studio)
  La ventana [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]Lista de errores**de** muestra los errores sintácticos y semánticos generados a partir del código de IntelliSense en el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="features-of-the-error-list"></a>Características de la ventana Lista de errores  
 La ventana **Lista de errores** proporciona la funcionalidad siguiente:  
  
-   A medida que se modifican los scripts, la **Lista de errores** muestra las advertencias y los errores generados por IntelliSense en el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Puede hacer doble clic en la entrada de cualquier mensaje de error para situarse en la pestaña del archivo de script que generó el error y desplazarse a la ubicación de éste.  
  
-   Puede filtrar las entradas que desea mostrar, así como las columnas de información que desea que aparezcan para cada entrada.  
  
-   Después de corregir un error, la entrada de error se elimina de la ventana **Lista de errores**.  
  
-   Al cerrar la pestaña para un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] , los errores generados en ese archivo se eliminan de la ventana **Lista de errores**.  
  
## <a name="working-with-the-error-list"></a>Trabajar con la ventana Lista de errores  
 Para mostrar la ventana **Lista de errores**, realice una de las siguientes operaciones:  
  
-   En el menú **Ver** , haga clic en **Lista de errores**.  
  
-   Use el método abreviado de teclado CTRL+\\, CTRL+E.  
  
 Después de abrir la ventana **Lista de errores**, puede personalizar la vista mediante las acciones siguientes:  
  
-   Para ordenar la lista, haga clic en cualquier encabezado de columna. Para ordenar de nuevo por una columna adicional, presione y mantenga presionada la tecla MAYÚS y, a continuación, haga clic en otro encabezado de columna.  
  
-   Para seleccionar qué columnas se muestran y cuáles están ocultas, seleccione **Mostrar columnas** en el menú de acceso directo.  
  
-   Para cambiar el orden en que se muestran las columnas, arrastre cualquier encabezado de columna hacia la izquierda o la derecha.  
  
 La ventana **Lista de errores** no incluye vínculos a información adicional sobre errores concretos.  
  
## <a name="transact-sql-errors-in-management-studio"></a>Errores de Transact-SQL en Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] muestra los errores para los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] en las ubicaciones siguientes:  
  
-   La ventana **Lista de errores** contiene todos los errores sintácticos y semánticos encontrados por IntelliSense en el Editor de [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Esta lista de errores se actualiza dinámicamente a medida que se modifican los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La lista incluye todos los errores encontrados por el editor en cada script de [!INCLUDE[tsql](../../includes/tsql-md.md)] . El editor no detiene el análisis de un archivo al encontrar errores en un script. En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], IntelliSense en el Editor de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no admite todos los elementos de sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] . La ventana **Lista de errores** solo contiene los errores de la sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] admitida por IntelliSense.  
  
-   La pestaña **Mensajes** de la parte inferior de ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestra todos los errores y los mensajes devueltos por [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] al ejecutar un script de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Esta lista no cambia hasta que se ejecuta el script de nuevo. [!INCLUDE[ssDE](../../includes/ssde-md.md)] detiene el análisis de un lote cuando encuentra uno o dos errores de compilación; por lo tanto, es posible que la pestaña **Mensajes** no incluya todos los errores de un script.  
  
 A veces, los errores aparecen en ambas ubicaciones. Por ejemplo, un archivo de script podría tener un error de sintaxis que apareciese en la ventana **Lista de errores**. Si ejecuta el script antes de corregir el error, el analizador de [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede detectar la misma condición y devolver otra copia del mensaje de error en la pestaña **Mensajes** .  
  
> [!NOTE]  
>  En **Lista de errores** solo se muestran los errores del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] ; no se muestran los errores de los editores MDX, DMX ni XML/A. Todos los errores de MDX, DMX y XML/A se muestran en la pestaña **Mensajes** de dichos editores.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 Cuando está abierta la ventana **Lista de errores** , la información se muestra en las columnas siguientes:  
  
 **Orden predeterminado**  
 Muestra un entero que indica el orden en el que se generó una entrada.  
  
 **Descripción**  
 Muestra el texto de la entrada de error. Las descripciones largas se ajustan a las líneas siguientes.  
  
 **Archivo**  
 Muestra el nombre del archivo de script que generó el error.  
  
 **Línea**  
 Muestra un entero que indica la línea de código que contiene el error.  
  
 **Columna**  
 Muestra un entero que indica la posición del error en la línea de código.  
  
 **Proyecto**  
 Muestra el nombre del proyecto que contiene el archivo de script.  
