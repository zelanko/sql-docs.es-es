---
title: Editor de consultas del motor de base de datos (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.tsqlquery.f1
dev_langs:
- TSQL
helpviewer_keywords:
- Query Editor [Database Engine]
- Transact-SQL Editor See Query Editor [Database Engine]
- Database Engine Query Editor See Query Editor [Database Engine]
- Query Editor [Database Engine], Toolbar
- editors [SQL Server Management Studio], Database Engine Query Editor
- Query Editor [Database Engine], Features
- SQL Server Management Studio [SQL Server], Database Engine Query Editor
ms.assetid: 05cfae9b-96d5-4a35-a098-0bc3a548bcfc
caps.latest.revision: 47
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 40ac7dd736d0366fe5cb564719a375e2e6a6a43d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="database-engine-query-editor-sql-server-management-studio"></a>Editor de consultas del motor de base de datos (SQL Server Management Studio)
  Use el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para crear y ejecutar scripts que contengan instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] . El editor también permite ejecutar scripts que contengan comandos **sqlcmd** .  
  
## <a name="transact-sql-f1-help"></a>Transact-SQL (Ayuda F1)  
 El editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] admite la vinculación al tema de referencia para una instrucción específica de [!INCLUDE[tsql](../../includes/tsql-md.md)] al presionar F1. Para ello, resalte el nombre de una instrucción Transact-SQL y presione F1. El motor de búsqueda de ayuda buscará un tema que tenga un atributo de Ayuda F1 que coincida con la cadena resaltada.  
  
 Si el motor de búsqueda de ayuda no encuentra un tema con una palabra clave de Ayuda F1 que coincida exactamente con la cadena resaltada, se mostrará este tema. En ese caso, hay dos métodos para encontrar la ayuda que busca:  
  
-   Copiar y pegar la cadena del editor que resaltó en la pestaña de búsqueda de los Libros en pantalla de SQL Server y realizar una búsqueda.  
  
-   Resaltar solo la parte de la instrucción Transact-SQL que sea más probable que coincida con una palabra clave de Ayuda F1 aplicada a un tema y vuelva a presionar F1. El motor de búsqueda requiere una correspondencia exacta entre la cadena resaltada y una palabra clave de Ayuda F1 asignada a un tema. Si la cadena resaltada contiene elementos únicos de su entorno, como nombres de columna o de parámetro, el motor de búsqueda no obtendrá una coincidencia. Entre los ejemplos de cadenas que se van a resaltar se incluyen los siguientes:  
  
    -   El nombre de una instrucción Transact-SQL, como SELECT, CREATE DATABASE o BEGIN TRANSACTION.  
  
    -   El nombre de una función integrada, como SERVERPROPERTY o @@VERSION.  
  
    -   El nombre de una tabla de procedimiento almacenado del sistema o de una vista, como sys.data_spaces o sp_tableoption.  
  
## <a name="working-with-the-database-engine-query-editor"></a>Trabajar con el editor de consultas del motor de base de datos  
 El editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] es uno de los cuatros editores implementados en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener una descripción de la funcionalidad implementada en el editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y las tareas principales que se pueden realizar mediante el editor, vea [Editores de consultas y texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md).  
  
## <a name="sql-editor-toolbar"></a>Barra de herramientas del Editor SQL  
 Cuando el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] está abierto, la barra de herramientas del Editor SQL aparece con los botones siguientes.  
  
 **Connect**  
 Se abre el cuadro de diálogo **Conectar al servidor** . Utilice este cuadro de diálogo para establecer una conexión a un servidor.  
  
 **Desconectar**  
 Desconecta el Editor de consultas actual del servidor.  
  
 **Cambiar conexión**  
 Se abre el cuadro de diálogo **Conectar al servidor** . Utilice este cuadro de diálogo para establecer una conexión a un servidor diferente.  
  
 **Consulta con conexión actual**  
 Abre una nueva ventana del Editor de consultas y usa la información de conexión de la ventana actual del Editor de consultas.  
  
 **Bases de datos disponibles**  
 Cambia la conexión a una base de datos distinta del mismo servidor.  
  
 **Execute**  
 Ejecuta el código seleccionado o, si no se ha seleccionado ningún código, ejecuta todo el código del Editor de consultas.  
  
 **Depuración**  
 Habilita el depurador de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este depurador admite acciones de depuración como establecer puntos de interrupción, inspeccionar variables y recorrer el código.  
  
 **Cancelar ejecución de la consulta**  
 Envía una solicitud de cancelación al servidor. Algunas consultas no pueden cancelarse inmediatamente, sino que deben esperar a una condición de cancelación adecuada. Cuando se cancelan las transacciones, podrían producirse retrasos mientras se revierten.  
  
 **Analizar**  
 Comprueba la sintaxis del código seleccionado. Si no se ha seleccionado ningún código, comprueba la sintaxis de todo el código en la ventana del Editor de consultas.  
  
 **Mostrar plan de ejecución estimado**  
 Solicita un plan de ejecución de consulta desde el procesador de consultas sin ejecutar realmente la consulta y muestra el plan en la ventana **Plan de ejecución** . Este plan utiliza estadísticas de índice para calcular el número de filas que se prevé que van a devolverse en cada parte de la ejecución de la consulta. El plan de consultas real que se utiliza puede ser diferente del plan de ejecución calculado. Esto puede ocurrir si el número de filas que se devuelven es significativamente diferente del calculado y el procesador de consultas cambia el plan para obtener una mayor eficacia.  
  
 **Opciones de consulta**  
 Abre el cuadro de diálogo **Opciones de consulta** . Use este cuadro de diálogo para configurar las opciones predeterminadas de la ejecución de consultas y los resultados de las mismas.  
  
 **IntelliSense habilitado**  
 Especifica si la funcionalidad de IntelliSense está disponible en el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 **Incluir plan de ejecución real**  
 Ejecuta la consulta, devuelve los resultados de la consulta y el plan de ejecución que se usó para la consulta. Se muestran como un plan de consultas gráfico en la ventana **Plan de ejecución** .  
  
 **Incluir estadísticas de cliente**  
 Incluye una ventana **Estadísticas de clientes** que contiene estadísticas sobre la consulta y los paquetes de red, así como el tiempo transcurrido de la consulta.  
  
 **Resultados a texto**  
 Devuelve los resultados de la consulta como texto en la ventana **Resultados** .  
  
 **Resultados a cuadrícula**  
 Devuelve los resultados de la consulta como una o varias cuadrículas en la ventana **Resultados** .  
  
 **Resultados a archivo**  
 Cuando se ejecuta la consulta, se abre el cuadro de diálogo **Guardar resultados** . En **Guardar en**, seleccione la carpeta en la que desea guardar el archivo. En **Nombre de archivo**, escriba el nombre del archivo y, a continuación, haga clic en **Guardar** para guardar los resultados de la consulta como un archivo **Informe** que tenga la extensión .rpt. Para obtener acceso a las opciones avanzadas, haga clic en la flecha abajo del botón **Guardar** y después haga clic en **Guardar con codificación**.  
  
 **Selección con comentarios**  
 Convierte la línea actual en comentario agregando al principio de la línea un operador de comentario (--).  
  
 **Selección sin comentarios**  
 Convierte la línea actual en una instrucción de código activo quitando los operadores de comentario (--) del principio de la línea.  
  
 **Reducir sangría de línea**  
 Mueve el texto de la línea a la izquierda quitando los espacios en blanco al principio de la línea.  
  
 **Aumentar sangría de línea**  
 Mueve el texto de la línea a la derecha agregando espacios en blanco al principio de la línea.  
  
 **Especificar valores para parámetros de plantilla**  
 Abre un cuadro de diálogo que puede utilizar para especificar los valores de los parámetros en los procedimientos almacenados y funciones.  
  
 También puede agregar la barra de herramientas del Editor SQL seleccionando el menú **Ver** y, a continuación, las opciones **Barras de herramientas**y **Editor SQL**. Si agrega la barra de herramientas del Editor SQL cuando no hay ninguna ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] abierta, no habrá ningún botón disponible.  
  
## <a name="sql-editor-toolbar"></a>Barra de herramientas del Editor SQL  
 Cuando se abre una ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , puede agregar la barra de herramientas Depurar seleccionando el menú **Ver** , seleccionando **Barras de herramientas**y seleccionando a continuación **Depurar**. Si agrega la barra de herramientas Depurar cuando no hay ninguna ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] abierta, no habrá ningún botón disponible.  
  
 **Continuar**  
 Ejecuta el código en la ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] hasta que se encuentre un punto de interrupción.  
  
 **Interrumpir todos**  
 Establece el depurador para interrumpir todos los procesos a los que está asociado cuando se produce una interrupción.  
  
 **Detener depuración**  
 Saca la ventana del Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] seleccionada del modo de depuración y restaura el modo de ejecución estándar.  
  
 **Mostrar la instrucción siguiente**  
 Mueve el cursor a la siguiente instrucción que se va a ejecutar.  
  
 **Paso a paso por instrucciones**  
 Se ejecuta la siguiente instrucción. Si la siguiente instrucción invoca un procedimiento almacenado, función o desencadenador de Transact-SQL, el depurador muestra una nueva ventana del **Editor de consultas** que contiene el código del módulo. La ventana está en el modo de depuración y la ejecución se detiene en la primera instrucción del módulo. Después puede desplazarse por el módulo, por ejemplo, estableciendo puntos de interrupción o recorriendo el código.  
  
 **Paso a paso por procedimientos**  
 Se ejecuta la siguiente instrucción. Si la instrucción invoca un procedimiento almacenado, una función o un desencadenador Transact-SQL, el módulo se ejecuta hasta que termine y los resultados se devuelven al código de llamada. Si está seguro de que no hay errores en el módulo, puede omitirlo. La ejecución se detiene en la instrucción que sigue a la llamada al módulo.  
  
 **Paso a paso para salir**  
 Vuelve al nivel de la siguiente llamada superior (función, procedimiento almacenado o desencadenador). La ejecución se detiene en la instrucción que sigue a la llamada al procedimiento almacenado, a la función o al desencadenador.  
  
 **Windows**  
 Abre la ventana **Punto de interrupción** o la ventana **Inmediato** .  
  
## <a name="see-also"></a>Vea también  
 [Métodos abreviados de teclado de SQL Server Management Studio](../../tools/sql-server-management-studio/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
