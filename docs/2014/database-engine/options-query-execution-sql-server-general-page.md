---
title: Opciones (ejecución de consultas-SQL Server-página general) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 83c0d1ad4d63d361754c5e2183081c30c7c51f2b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089992"
---
# <a name="options-query-execution-sql-server-general-page"></a>Opciones (ejecución de consultas-SQL Server-página general)
  Use esta página para especificar las opciones de ejecución de consultas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Los cambios que se realicen en estas opciones solo se aplicarán a las nuevas consultas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para cambiar las opciones de una consulta actual, haga clic en **Opciones de consulta** en el menú **Consulta** o, en una ventana Consulta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], haga clic con el botón derecho y seleccione **Opciones de consulta**.  
  
## <a name="options"></a>Opciones  
 **ESTABLECER ROWCOUNT**  
 El valor predeterminado 0 indica que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esperará a que se reciban todos los resultados. Especifique un valor mayor que 0 si desea que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] detenga la consulta después de obtener el número de filas especificado. Para desactivar esta opción (de modo que se devuelvan todas las filas), especifique SET ROWCOUNT 0.  
  
 **ESTABLECER TEXTSIZE**  
 El valor predeterminado de 2.147.483.647 bytes indica que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporcionará campos de datos completos hasta el límite de los campos de datos `text` y `ntext`. Especifique un número menor para limitar los resultados en caso de que los valores sean elevados. Las columnas que superen el número especificado se truncarán.  
  
 **Tiempo de espera de ejecución**  
 Establece el valor predeterminado en el cuadro de diálogo **Nueva conexión** . Utilice este cuadro de número para indicar a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] el número de segundos que debe esperar antes de cancelar la consulta. Un valor de 0 indica una espera infinita o ningún tiempo de espera. Este valor es 0 en una nueva instalación.  
  
 **Separador de lotes**  
 Escriba la palabra que utilice para separar instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] en lotes. El separador predeterminado es GO.  
  
 **De forma predeterminada, abrir nuevas consultas en modo SQLCMD**  
 Active esta casilla para abrir nuevas consultas en modo SQLCMD. Para obtener más información sobre el modo SQLCMD, vea [editar scripts SQLCMD con el editor de consultas](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md).  
  
 Cuando seleccione esta opción, tenga en cuenta las siguientes limitaciones:  
  
-   IntelliSense se desactiva en el Editor de consultas de [!INCLUDE[ssDE](../includes/ssde-md.md)] .  
  
-   Debido a que el Editor de consultas no se ejecuta desde la línea de comandos, no podrá pasar parámetros de línea de comandos, tales como variables.  
  
-   Dado que el Editor de consultas no puede responder a comandos del sistema operativo, debe tener cuidado de no ejecutar instrucciones interactivas.  
  
 **Restablecer valores predeterminados**  
 Haga clic en esta opción para restablecer todos los valores de esta página a los valores predeterminados originales.  
  
## <a name="see-also"></a>Consulte también  
 [Utilidad sqlcmd](../tools/sqlcmd-utility.md)  
  
  
