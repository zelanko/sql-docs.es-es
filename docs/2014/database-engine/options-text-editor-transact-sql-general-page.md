---
title: Opciones (editor de texto-Transact-SQL-página general) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.SQL.General
dev_langs:
- TSQL
ms.assetid: 7021ecb7-8fb5-4d8c-b984-3d34fcde8be2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: f32377fffb26ac622dc4045d108e491adc2b0342
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089170"
---
# <a name="options-text-editor---transact-sql--general-page"></a>Opciones (editor de texto-Transact-SQL-página general)
  Utilice el cuadro de diálogo **General** para cambiar el comportamiento general de la edición del Editor de consultas del [!INCLUDE[ssDE](../includes/ssde-md.md)] , que se utiliza para modificar los scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] . Para mostrar esta configuración, haga clic en **Opciones** en el menú **Herramientas**, expanda la subcarpeta **Transact-SQL** y luego haga clic en **General**.  
  
## <a name="setting-options-in-multiple-locations"></a>Establecer opciones en varias ubicaciones  
 Las opciones del [!INCLUDE[ssDE](../includes/ssde-md.md)] editor de consultas también se pueden establecer en el cuadro de diálogo **General de todos los idiomas** . Si usa los cuadros de diálogo **todos los lenguajes** para establecer diferentes opciones para [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] los demás editores, como los editores DMX o MDX, debe restablecer las [!INCLUDE[ssDE](../includes/ssde-md.md)] opciones del editor de consultas mediante este cuadro de diálogo.  
  
## <a name="statement-completion"></a>Finalización de instrucciones  
 **Lista de miembros automática**  
 Cuando se activa esta casilla, se muestran las listas de objetos de base de datos y de esquema, columnas, funciones con valores de tabla o funciones disponibles a medida que se escribe en el editor. Elija cualquier elemento de la lista desplegable para insertarlo en el código.  
  
 **Ocultar miembros avanzados**  
 Esta casilla no está disponible.  
  
 **Información de parámetros**  
 Cuando se selecciona esta casilla, se muestra información sobre los parámetros para una función o un procedimiento almacenado que se encuentre inmediatamente a la izquierda del punto de inserción (cursor). Esta información incluye una lista de todos los parámetros disponibles con sus nombres y tipos de datos.  
  
## <a name="settings"></a>Configuración  
 **Habilitar espacio virtual**  
 Cuando esta casilla está activada, puede hacer clic en cualquier parte situada más allá del final de una línea de código y escribir. Seleccione esta casilla para colocar comentarios en un punto coherente junto al código. Si se activa esta casilla, se deshabilita la casilla **Ajuste de línea** .  
  
 **Ajuste de palabra**  
 Cuando se selecciona esta casilla, cualquier parte de una línea que se extienda horizontalmente fuera del área visible del editor se mostrará automáticamente en la siguiente línea. La activación de esta casilla habilita la casilla **Mostrar glifos visuales para ajuste de línea** y deshabilita la casilla **Habilitar espacio virtual** .  
  
 **Mostrar glifos visuales para ajuste de línea**  
 Cuando esta casilla está activada, aparecerá un indicador de flecha de retorno donde una línea larga se ajusta respecto a la línea siguiente.  
  
 **Aplicar comandos Cortar o Copiar a líneas en blanco si no hay selección**  
 Esta casilla establece el comportamiento del editor cuando el punto de inserción se coloca en una línea en blanco, no se selecciona nada y se hace clic en **Copiar** o **Cortar**.  
  
 Cuando se selecciona esta casilla, se copia o se corta la línea en blanco. Si luego hace clic en **Pegar**, se insertará una nueva línea en blanco.  
  
 Cuando esta casilla está desactivada, no se copia o se corta nada. Si luego hace clic en **Pegar**, se pegará el contenido de la última copia. Si previamente no se ha copiado nada, no se pegará nada.  
  
 Esta configuración no tiene efecto en **Copiar** o **Cortar** cuando una línea no está en blanco. Si no se selecciona nada, se copia o se corta la línea entera. Si luego hace clic en **Pegar**, se pegará el texto de toda la línea y su carácter de final de línea.  
  
## <a name="display"></a>Pantalla  
 **Números de línea**  
 Cuando se selecciona esta casilla, aparecerá un número de línea junto a cada línea de código.  
  
> [!NOTE]  
>  Estos números de línea no se agregan al código y no se imprimen. Solo sirven como referencia.  
  
 **Habilitar acceso a direcciones URL con un solo clic**  
 Cuando se selecciona esta casilla, el cursor cambia a una mano cuando pasa por encima de una dirección URL en el editor. Puede hacer clic en la dirección URL para abrir la página indicada en el explorador web.  
  
 **Barra de navegación**  
 Esta casilla no está disponible.  
  
  
