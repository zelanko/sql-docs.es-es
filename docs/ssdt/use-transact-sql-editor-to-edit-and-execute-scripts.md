---
title: Usar el Editor de Transact-SQL para editar y ejecutar scripts
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLEDITOR
ms.assetid: fa78e2cf-3c64-49f5-93cc-a3d50b1e7d05
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: c3eaaa53b87d2e360503a087b8978f507d6a6023
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75256200"
---
# <a name="use-transact-sql-editor-to-edit-and-execute-scripts"></a>Usar el Editor de Transact-SQL para editar y ejecutar scripts

El Editor de Transact\-SQL le ofrece una experiencia completa de edición y depuración cuando trabaja con scripts. Se invoca cuando se usa el menú contextual **Ver código** para abrir una entidad de base de datos en una base de datos conectada o en un proyecto. También se abre automáticamente cuando se usa el menú contextual **Nueva consulta** desde el Explorador de objetos de SQL Server o cuando se agrega un nuevo objeto de script a un proyecto de base de datos.  
  
Si no está conectado a una base de datos pero desea ejecutar una consulta en ella, también puede usar el cuadro de diálogo **Nueva conexión de consulta** en la opción de menú **SQL** -> **Editor de Transact\-SQL** para conectar con una base de datos e iniciar el Editor de Transact\-SQL.  
  
El Editor de Transact\-SQL contiene un panel de **T-SQL** principal donde puede escribir y editar scripts de Transact\-SQL. El editor admite IntelliSense y codificación en colores de la sintaxis para mejorar la legibilidad de las instrucciones complejas. También admite búsqueda y reemplazo, marcado como comentarios masivo, fuentes y colores personalizados, y numeración de líneas. Asimismo, puede cambiar la base de datos en la que se ejecutará el script en el editor. Para obtener más información, consulte [Clonación de una conexión a una base de datos](../ssdt/how-to-clone-an-existing-database.md). El panel **Resultados** muestra los resultados de la consulta en una cuadrícula o texto. También puede redirigir los resultados de la consulta a un archivo. El panel **Mensaje** muestra errores, advertencias y mensajes informativos que se devuelven cuando se ejecuta un script. Cuando las estadísticas de cliente están habilitadas, el panel **Estadísticas** muestra información sobre la ejecución de la consulta agrupada en categorías. El panel **Plan de ejecución** muestra los métodos de recuperación de datos elegidos por SQL Server, así como el costo de ejecución de determinadas instrucciones y consultas.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|---------|---------------|  
|[Cómo: Esquematizar y agregar fragmentos de código a script Transact-SQL](../ssdt/how-to-outline-and-add-snippets-to-transact-sql-script.md)|Usar el Selector de fragmentos de código para insertar en la consulta código de Transact\-SQL ya preparado.|  
|[Cómo: Navegar entre scripts](../ssdt/how-to-navigate-between-scripts.md)|Usar Ir a la definición y Buscar todas las referencias para navegar entre scripts.|  
|[Cómo: Usar Cambiar nombre y Refactorizar para realizar cambios en los objetos de base de datos](../ssdt/how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects.md)|Cambiar el nombre de un objeto en todos los scripts y obtener una vista previa de los cambios.|  
|[Cómo: Ejecutar una consulta parcial](../ssdt/how-to-execute-a-partial-query.md)|Resaltar un segmento específico del script y ejecutarlo como una única consulta.|  
|[Cómo: Depurar procedimientos almacenados](../ssdt/how-to-debug-stored-procedures.md)|Crear y depurar un procedimiento almacenado de Transact\-SQL depurando paso a paso por instrucciones.|  
|[Analizar el rendimiento de los scripts](../ssdt/analyze-script-performance.md)|Usar planes de ejecución, estadísticas de cliente y análisis de código para determinar si puede mejorar el rendimiento de la consulta, los procedimientos almacenados o los scripts.|  
  
## <a name="see-also"></a>Consulte también

[Cómo: Crear nuevos objetos de base de datos mediante consultas](../ssdt/how-to-create-new-database-objects-using-queries.md)