---
title: Ejecución de opciones de consulta (página general) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.general.f1
ms.assetid: 858a0263-2f04-4692-b8bf-63e93c998ead
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b3ecf106315fa88fdfb68599cfce71a77be975dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089043"
---
# <a name="query-options-execution-general-page"></a>Ejecución de Opciones de consulta (página General)
  Utilice esta página para especificar las opciones de ejecución [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de consultas. Para tener acceso a este cuadro de diálogo, haga clic con el botón derecho en el cuerpo de una ventana del Editor de consultas y haga clic en **Opciones de consulta**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **ESTABLECER ROWCOUNT**  
 El valor predeterminado 0 indica que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esperará a que se reciban todos los resultados. Especifique un valor mayor que 0 si desea que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] detenga la consulta después de obtener el número de filas especificado. Para desactivar esta opción (de modo que se devuelvan todas las filas), especifique SET ROWCOUNT 0.  
  
 **ESTABLECER TEXTSIZE**  
 El valor predeterminado, 2.147.483.647 bytes, indica que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporcionará un campo de datos completo hasta el límite de los campos de datos `text`, `ntext`, `nvarchar(max)` y `varchar(max)`. No afecta al tipo de datos XML. Especifique un número menor para limitar los resultados en caso de que los valores sean elevados. Las columnas que superen el número especificado se truncarán.  
  
 **Tiempo de espera de ejecución**  
 Indica el número de segundos de espera antes de cancelar la consulta. El valor 0 indica una espera infinita o que no hay tiempo de espera.  
  
 **Separador de lotes**  
 Escriba la palabra que utilice para separar instrucciones Transact-SQL en lotes. El separador predeterminado es GO.  
  
 **De forma predeterminada, abrir nuevas consultas en modo SQLCMD**  
 Active esta casilla para abrir nuevas consultas en modo SQLCMD. Esta casilla solo se muestra cuando el cuadro de diálogo se abre desde el menú **Herramientas** .  
  
 Cuando seleccione esta opción, tenga en cuenta las siguientes limitaciones:  
  
-   IntelliSense se desactiva en el Editor de consultas de [!INCLUDE[ssDE](../includes/ssde-md.md)] .  
  
-   Debido a que el Editor de consultas no se ejecuta desde la línea de comandos, no podrá pasar parámetros de línea de comandos, tales como variables.  
  
-   Dado que el Editor de consultas no puede responder a comandos del sistema operativo, debe tener cuidado de no ejecutar instrucciones interactivas.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
