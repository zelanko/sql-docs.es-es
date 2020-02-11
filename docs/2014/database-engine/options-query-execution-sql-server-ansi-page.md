---
title: Opciones (ejecución de consultas-SQL Server-página ANSI) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAnsi
ms.assetid: 0f4c6887-0562-417e-806c-b5cffb1e7c5c
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: e075de106a66ffee63c02ead06a3fc68548111a8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089379"
---
# <a name="options-query-execution-sql-server-ansi-page"></a>Opciones (ejecución de consultas-SQL Server-página ANSI)
  Conjuntamente, estas opciones SET del estándar ANSI (ISO) definen el entorno de procesamiento de consultas durante la consulta del usuario, la ejecución de un desencadenador o un procedimiento almacenado. Sin embargo, estas opciones SET no son todas las necesarias para ajustarse al estándar ISO. Use esta página para especificar que [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ejecutará las consultas utilizando todos o parte de los valores de configuración especificados en el estándar ISO. Los cambios que se realicen en estas opciones solo se aplicarán a las nuevas consultas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para cambiar las opciones de las consultas actuales, haga clic en **Opciones de consulta** en el menú **consulta** o haga clic con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] el botón secundario en la ventana de consulta y seleccione **Opciones de consulta**. En el cuadro de diálogo **Opciones de consulta** , en **Ejecución**, haga clic en **ANSI**.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **ESTABLECER ANSI_DEFAULTS**  
 Active esta casilla para seleccionar todos los valores de configuración predeterminados ISO. No todas las opciones ISO están seleccionadas de forma predeterminada.  
  
 **SET QUOTED_IDENTIFIER**  
 Cuando esta casilla está activada, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aplica las reglas ISO relativas a los identificadores delimitados por comillas y a las cadenas literales. Los identificadores delimitados por comillas pueden ser palabras clave reservadas de Transact-SQL o pueden contener caracteres no admitidos normalmente por las reglas de sintaxis de Transact-SQL para identificadores. Esta casilla está activada de forma predeterminada.  
  
 **SET ANSI_NULL_DFLT_ON**  
 Cuando se establece este valor, todas las columnas o tipos de datos definidos por el usuario que no se hayan especificado explícitamente como NOT NULL en una instrucción CREATE TABLE o ALTER TABLE admitirán valores NULL de forma predeterminada. Esta casilla está activada de forma predeterminada.  
  
 **SET IMPLICIT_TRANSACTIONS**  
 Cuando esta casilla está activada, SET IMPLICIT_TRANSACTIONS establece la conexión en el modo de transacción implícita. Cuando esta casilla se desactiva, restablece la conexión al modo de transacción con confirmación automática. Para revisar las instrucciones que inician una transacción implícita cuando están seleccionadas, vea [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-implicit-transactions-transact-sql). Esta casilla está desactivada de forma predeterminada.  
  
 **SET CURSOR_CLOSE_ON_COMMIT**  
 Cuando esta casilla está activada, cualquier cursor abierto se cierra automáticamente (de conformidad con ISO) al confirmarse una transacción. Cuando este valor se establece en OFF, los cursores permanecen abiertos a lo largo de los límites de las transacciones y solo se cierran cuando termina la conexión o cuando se cierran de manera explícita. Esta casilla está desactivada de forma predeterminada.  
  
 **SET ANSI_PADDING**  
 Controla el modo en que la columna almacena nombres de valor más cortos que el tamaño definido y el modo en que almacena valores con espacios en blanco finales en datos de tipo **char**, **varchar**, **binary**y **varbinary** . Esta opción solo afecta a la definición de nuevas columnas. Una vez creada la columna, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] almacena los valores de acuerdo con la opción establecida en el momento de su creación. Las columnas existentes no se ven afectadas por los cambios posteriores de esta opción. Esta casilla está activada de forma predeterminada.  
  
 **SET ANSI_WARNINGS**  
 Especifica el comportamiento estándar ISO para diversas condiciones de error:  
  
-   Cuando esta casilla está activada, si aparecen valores NULL en funciones de agregado (como SUM, AVG, MAX, MIN, STDEV, STDEVP, VAR, VARP o COUNT), se genera un mensaje de advertencia. Cuando es OFF, no se genera ninguna advertencia.  
  
-   Cuando esta casilla está desactivada, los errores de división por cero y desbordamiento aritmético hacen que la instrucción se revierta y que se genere un mensaje de error. Cuando es OFF, los errores de división por cero y de desbordamiento aritmético hacen que se devuelvan valores NULL. El comportamiento por el que un error de división por cero o desbordamiento aritmético hace que se devuelvan valores NULL tiene lugar cuando se intenta ejecutar una operación INSERT o UPDATE en una columna de tipo **character**, **Unicode** o **binary**, en la que la longitud del nuevo valor excede el tamaño máximo de la columna. Si SET ANSI_WARNINGS es ON, la operación INSERT o UPDATE se cancela, tal y como especifica el estándar ISO. No se tienen en cuenta los espacios en blanco a la derecha en las columnas de carácter ni los valores NULL a la derecha en las columnas binarias. Cuando es OFF, los datos se truncan para ajustarlos al tamaño de la columna y la instrucción se ejecuta correctamente.  
  
 Esta casilla está activada de forma predeterminada.  
  
 **SET ANSI_NULLS**  
 -   Especifica el comportamiento conforme a ISO de los operadores de comparación Es igual a (=) y No es igual a (<>) cuando se utilizan con valores NULL. Cuando la opción SET ANSI_NULLS está seleccionada, todas las comparaciones con un valor NULL se evalúan como UNKNOWN, el comportamiento conforme a ISO. Cuando la opción SET ANSI_NULLS no está seleccionada, la comparación de cualquier dato con un valor NULL se evalúa como TRUE. Esta casilla está activada de forma predeterminada.  
  
 **Restablecer valores predeterminados**  
 Restablece todos los valores de esta página a los valores predeterminados originales.  
  
  
