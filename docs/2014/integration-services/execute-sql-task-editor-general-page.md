---
title: Ejecutar el Editor de la tarea SQL (página General) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.general.f1
helpviewer_keywords:
- Execute SQL Task Editor
ms.assetid: beb39086-28ce-46af-b6d8-f7b4fb8d9069
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 559f13c3c777931270f4bc289f890f2360361030
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62898843"
---
# <a name="execute-sql-task-editor-general-page"></a>Editor de la tarea Ejecutar SQL (página General)
  Use la página **General** del cuadro de diálogo **Editor de la tarea Ejecutar SQL** para configurar la tarea Ejecutar SQL y proporcionar la instrucción SQL de ejecución de la tarea.  
  
 Para obtener información sobre esta tarea, vea [Tarea Ejecutar SQL](control-flow/execute-sql-task.md), [Parámetros y códigos de retorno en la tarea Ejecutar SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) y [Conjuntos de resultados en la tarea Ejecutar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md). Para más información sobre el lenguaje de consultas Transact-SQL y su sintaxis, vea [Referencia de Transact-SQL &#40;motor de base de datos&#41;](/sql/t-sql/language-reference).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Name**  
 Escriba un nombre único para la tarea Ejecutar SQL en el flujo de trabajo. El nombre que indique se mostrará en el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descripción**  
 Describa la tarea Ejecutar SQL. Como práctica recomendada, describa la tarea en función de su objetivo para que los paquetes se autodocumenten y su mantenimiento resulte sencillo.  
  
 **TimeOut**  
 Especifique la duración máxima en segundos de la ejecución de la tarea antes de exceder el tiempo de espera. Un valor de 0 indica un tiempo infinito. El valor predeterminado es 0.  
  
> [!NOTE]  
>  En los procedimientos almacenados no se excederá el tiempo de espera si imitan la funcionalidad de espera al proporcionar un tiempo para la realización de conexiones y finalización de las transacciones superior al número de segundos especificado en **TimeOut**. Sin embargo, los procedimientos almacenados que ejecutan consultas siempre están sujetos a la restricción de tiempo especificada en **TimeOut**.  
  
 **CodePage**  
 Especifique la página de códigos que desea utilizar para traducir los valores Unicode a variables. El valor predeterminado es la página de códigos del equipo local.  
  
> [!NOTE]  
>  Cuando la tarea Ejecutar SQL utiliza un administrador de conexiones ADO u ODBC, la propiedad **CodePage** no está disponible. Si la solución requiere el uso de una página de códigos, utilice un administrador de conexiones OLE DB o ADO.NET con la tarea Ejecutar SQL.  
  
 **TypeConversionMode**  
 Cuando establece esta propiedad en `Allowed`, la tarea Ejecutar SQL intentará convertir el parámetro de salida y los resultados de la consulta al tipo de datos de la variable a la que se asignan los resultados. Esto se aplica al tipo de conjunto de resultados de **Fila única** .  
  
 **ResultSet**  
 Especifique el tipo de resultados esperado tras la ejecución de la instrucción SQL. Elija **Fila única**, **Conjunto de resultados completo**, **XML**o **Ninguno**.  
  
 **ConnectionType**  
 Elija el tipo de administrador de conexiones que desea utilizar para conectarse al origen de datos. Entre los tipos de conexión disponibles se encuentran **OLE DB**, **ODBC**, **ADO**, **ADO.NET** y **SQLMOBILE**.  
  
 **Temas relacionados:** [Administrador de conexiones OLE DB](connection-manager/ole-db-connection-manager.md), [Administrador de conexiones ODBC](connection-manager/odbc-connection-manager.md), [Administrador de conexiones ADO](connection-manager/ado-connection-manager.md), [Administrador de conexiones ADO.NET](connection-manager/ado-net-connection-manager.md), [Administrador de conexiones con SQL Server Compact Edition](connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Conexión**  
 Elija la conexión en la lista de administradores de conexión definidos. Para crear una conexión, seleccione \<**Nueva conexión…**>.  
  
 **SQLSourceType**  
 Seleccione el tipo de origen de la instrucción SQL que ejecuta la tarea.  
  
 Dependiendo del tipo de administrador de conexiones que utiliza la tarea Ejecutar SQL, debe utilizar marcadores de parámetros específicos en instrucciones SQL con parámetros.  
  
 **Temas relacionados:** Sección de comandos SQL con parámetros de ejecución en [tarea Ejecutar SQL](control-flow/execute-sql-task.md)  
  
 Esta propiedad presenta las opciones indicadas en la siguiente tabla.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Entrada directa**|Establezca el origen para una instrucción Transact-SQL. Si selecciona este valor, se mostrará la opción dinámica **SQLStatement**.|  
|**Conexión de archivos**|Seleccione un archivo que contenga una instrucción Transact-SQL. Si selecciona esta opción, se mostrará la opción dinámica **FileConnection**.|  
|**Variable**|Establezca el origen a una variable que defina la instrucción Transact-SQL. Si selecciona este valor, se mostrará la opción dinámica **SourceVariable**.|  
  
 **QueryIsStoredProcedure**  
 Indica que la instrucción SQL especificada es un procedimiento almacenado. Esta propiedad es de solo lectura/escritura si la tarea utiliza el administrador de conexiones ADO. Si no es el caso, la propiedad es de solo lectura y su valor es `false`.  
  
 **BypassPrepare**  
 Indique si la instrucción SQL está preparada.  `true` omite la preparación; `false` prepara la instrucción SQL antes de ejecutarla. Esta opción solo estará disponible con las conexiones OLE DB que admiten la preparación.  
  
 **Temas relacionados:**  [Ejecución preparada](../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Examinar**  
 Busque un archivo que contenga una instrucción SQL en el cuadro de diálogo **Abrir** . Seleccione el archivo en el que desea copiar el contenido del archivo como una instrucción SQL en la propiedad **SQLStatement** .  
  
 **Generar consulta**  
 Cree una instrucción SQL con el cuadro de diálogo **Generador de consultas** , una herramienta gráfica usada para crear consultas. Esta opción estará disponible si la opción **SQLSourceType** se establece en **Entrada directa**.  
  
 **Analizar consulta**  
 Valide la sintaxis de la instrucción SQL.  
  
## <a name="sqlsourcetype-dynamic-options"></a>Opciones dinámicas de SQLSourceType  
  
### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Entrada directa  
 **SQLStatement**  
 Escriba la instrucción SQL que quiere ejecutar en el cuadro de opción, o bien haga clic en el botón Examinar […] para escribir la instrucción SQL en el cuadro de diálogo **Escribir consulta SQL**; también puede hacer clic en **Generar consulta** para escribir la instrucción en el cuadro de diálogo **Generador de consultas**.  
  
 **Temas relacionados:** [Generador de consultas](../../2014/integration-services/query-builder.md)  
  
### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = Conexión de archivos  
 **FileConnection**  
 Seleccione un administrador de conexiones de archivos existente o haga clic en \<**Nueva conexión...**> para crear un nuevo administrador de conexiones.  
  
 **Temas relacionados:** [Administrador de conexiones de archivos](connection-manager/file-connection-manager.md), [Editor de administrador de conexiones de archivos](../../2014/integration-services/file-connection-manager-editor.md)  
  
### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variable  
 **SourceVariable**  
 Seleccione una variable existente o haga clic en \<**Nueva variable…**> para crear una.  
  
 **Temas relacionados:** [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Agregar variable](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Ejecutar el Editor de la tarea SQL &#40;página asignación de parámetros&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)   
 [Ejecutar el Editor de la tarea SQL &#40;página conjunto de resultados&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
  
