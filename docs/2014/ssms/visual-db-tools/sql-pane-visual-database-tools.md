---
title: Panel SQL (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Query Designer [SQL Server], SQL pane
- View Designer, SQL pane
- SQL pane [Visual Database Tools]
ms.assetid: dbabab18-0614-415b-a2ef-9bcd0d320d5c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd223c0a66b533cb2b405dd0e766f7053b7a4e89
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63275964"
---
# <a name="sql-pane-visual-database-tools"></a>Panel SQL (Visual Database Tools)
  Puede utilizar el panel SQL para crear su propia instrucción SQL o puede hacerlo en los paneles Criterios y Diagrama (en ese caso, las instrucciones SQL se crearán en el panel SQL). A medida que crea la consulta, el panel SQL actualiza la instrucción y le vuelve a dar formato automáticamente para facilitar su lectura.  
  
 Para abrir el panel SQL, primero abra el Diseñador de consultas y vistas (con un objeto de base de datos seleccionado en Explorador de servidores, en el menú **Base de datos** haga clic en **Nueva consulta**). A continuación, en el menú **Diseñador de consultas** , seleccione **Panel** y haga clic en **SQL**.  
  
 En el panel SQL, puede:  
  
-   Crear consultas nuevas mediante la especificación de instrucciones SQL.  
  
-   Modificar la instrucción SQL creada por el Diseñador de consultas y vistas a partir de la configuración establecida en los paneles Diagrama y Criterios.  
  
-   Especificar instrucciones que aprovechan las ventajas de las características específicas de la base de datos que está utilizando.  
  
> [!NOTE]  
>  Asegúrese de que conoce las reglas para identificar objetos de base de datos en la base de datos que está utilizando. Para obtener información detallada, vea la documentación del sistema de administración de bases de datos.  
  
## <a name="statements-in-the-sql-pane"></a>Instrucciones en el panel SQL  
 Puede modificar la consulta actual directamente en el panel SQL. Al desplazarse a otro panel, el Diseñador de consultas y vistas da formato a la instrucción de forma automática y, a continuación, cambia los paneles Diagrama y Criterios para que coincidan con la instrucción.  
  
 Si la instrucción no puede representarse en los paneles Diagrama y Criterios y éstos están visibles, el Diseñador de consultas y vistas mostrará un error y, a continuación, ofrecerá dos alternativas:  
  
-   Omitir el hecho que la instrucción no puede representarse en los paneles Diagrama y Criterios.  
  
-   Deshacer el cambio que no puede representarse y revertir la instrucción SQL a su versión más reciente.  
  
 Si decide omitir el hecho de que la instrucción no puede representarse en los paneles Diagrama y Criterios, el Diseñador de consultas y vistas atenuará los otros paneles para indicar que ya no reflejan el contenido del panel SQL.  
  
 Puede continuar con la modificación de la instrucción y ejecutarla como lo haría con cualquier otra instrucción SQL.  
  
> [!NOTE]  
>  Si especifica una instrucción SQL, pero, a continuación, realiza cambios adicionales en la consulta mediante la modificación de los paneles Diagrama y Criterios, el Diseñador de consultas y vistas vuelve a generar y a mostrar la instrucción SQL. En algunos casos, esta acción da como resultado una instrucción SQL construida de forma diferente a la que especificó originalmente (aunque siempre dará los mismos resultados). Es especialmente probable que se produzca esta diferencia cuando está trabajando con condiciones de búsqueda que incluyen varias cláusulas vinculadas con AND y OR.  
  
## <a name="see-also"></a>Vea también  
 [Crear consultas &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Ejecutar consultas &#40;Visual Database Tools&#41;](run-queries-visual-database-tools.md)   
 [Diseñar temas de procedimientos de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [Panel de diagrama &#40;Visual Database Tools&#41;](diagram-pane-visual-database-tools.md)   
 [Panel criterios &#40;Visual Database Tools&#41;](criteria-pane-visual-database-tools.md)   
 [Panel Resultados &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md)  
  
  
