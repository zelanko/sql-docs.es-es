---
title: Crear bucles entre archivos y tablas de Excel mediante un contenedor de bucles Para cada uno | Microsoft Docs
ms.custom: ''
ms.date: 05/15/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: a5393c1a-cc37-491a-a260-7aad84dbff68
caps.latest.revision: 35
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 19ecd67f514c812745e161f353e71d0037ffe783
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35401067"
---
# <a name="loop-through-excel-files-and-tables-by-using-a-foreach-loop-container"></a>Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach
  Los procedimientos de este tema explican cómo crear bucles entre libros de Excel en una carpeta o entre tablas en un libro de Excel, mediante el contenedor de bucles Foreach con el enumerador correspondiente.  

> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).
 
## <a name="to-loop-through-excel-files-by-using-the-foreach-file-enumerator"></a>Para crear un bucle entre libros de Excel con el enumerador de archivos para Foreach  
  
1.  Cree una variable de cadena que recibirá la ruta de acceso y nombre de archivo de Excel actuales en cada iteración del bucle. Para evitar problemas de validación, asigne una ruta de acceso y un nombre de archivo de Excel válidos como valor inicial de la variable (la expresión de ejemplo que se muestra más adelante en este procedimiento utiliza el nombre de variable `ExcelFile`).  
  
2.  También puede crear otra variable de cadena que mantendrá el valor del argumento Propiedades extendidas de la cadena de conexión de Excel. Este argumento contiene una serie de valores que especifican la versión de Excel y determinan si la primera fila contiene nombres de columna, y si se utiliza un modo de importación (la expresión de ejemplo que se muestra más adelante en este procedimiento utiliza el nombre de variable `ExtProperties`, con un valor inicial de "`Excel 12.0;HDR=Yes`").  
  
     Si no usa una variable para el argumento Propiedades extendidas, debe agregarlo manualmente a la expresión que contiene la cadena de conexión.  
  
3.  Agregue un contenedor de bucles Foreach a la pestaña **Flujo de control** . Para obtener más información sobre cómo configurar el contenedor de bucles Foreach, vea [Configurar un contenedor de bucles Foreach](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
4.  En la página **Colección** del **Editor de bucles Foreach**, seleccione el enumerador de archivos para Foreach, especifique la carpeta en la que se encuentran los libros de Excel e indique el filtro de archivos (generalmente *.xlsx).  
  
5.  En la página **Asignaciones de variables** , asigne Índice 0 a una variable de cadena definida por el usuario que recibirá la ruta de acceso y el nombre de archivo de Excel actuales en cada iteración del bucle. (La expresión de ejemplo que se muestra más adelante en este procedimiento utiliza el nombre de variable `ExcelFile`.)  
  
6.  Cierre el **Editor de bucles Foreach**.  
  
7.  Agregue un administrador de conexiones con Excel al paquete como se describe en [Agregar, eliminar o compartir un administrador de conexiones en un paquete](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655). Seleccione un libro de Excel existente para la conexión a fin de evitar que se produzcan errores de validación.  
  
    > [!IMPORTANT]  
    >  Para evitar que se produzcan errores de validación al configurar tareas y componentes de flujo de datos que utilizan este administrador de conexiones con Excel, seleccione un libro de Excel existente en el **Editor del Administrador de conexiones con Excel**. El administrador de conexiones no utilizará ese libro en tiempo de ejecución después de configurar una expresión para la propiedad **ConnectionString** como se describe en los pasos siguientes. Tras crear y configurar el paquete, puede borrar el valor de la propiedad **ConnectionString** en la ventana Propiedades. Sin embargo, si borra este valor, la propiedad de cadena de conexión del administrador de conexiones de Excel deja de ser válido hasta que se ejecuta el bucle Foreach. Por lo tanto, debe establecer la propiedad **DelayValidation** en **True** en las tareas en las que se utiliza el administrador de conexiones, o bien en el paquete, para evitar errores de validación.  
    >   
    >  También debe utilizar el valor predeterminado de **False** para la propiedad **RetainSameConnection** del administrador de conexiones de Excel. Si cambia este valor a **True**, cada iteración del bucle continuará abriendo el primer libro de Excel.  
  
8.  Seleccione el nuevo administrador de conexiones de Excel, haga clic en la propiedad **Expresiones** en la ventana Propiedades y luego haga clic en los puntos suspensivos.  
  
9. En el **Editor de expresiones de propiedad**, seleccione la propiedad **ConnectionString** y haga clic en los puntos suspensivos.  
  
10. En el Generador de expresiones, escriba la siguiente expresión:  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=\"" + @[User::ExtProperties] + "\""  
    ```  
  
     Observe el uso del carácter de escape "\\" para las comillas internas necesarias en el valor del argumento Propiedades extendidas.  
  
     El argumento Propiedades extendidas no es opcional. Si no usa una variable para contener su valor, debe agregarlo manualmente a la expresión, como en el ejemplo siguiente:  
  
    ```  
    "Provider=Microsoft.ACE.OLEDB.12.0;Data Source=" +  @[User::ExcelFile] + ";Extended Properties=Excel 12.0"  
    ```  
  
11. Cree tareas en el contenedor de bucles Foreach que utilicen el administrador de conexiones con Excel para realizar las mismas operaciones en cada libro de Excel que coincida con la ubicación y el patrón del archivo especificados.  
  
## <a name="to-loop-through-excel-tables-by-using-the-foreach-adonet-schema-rowset-enumerator"></a>Para crear un bucle entre tablas de Excel con el enumerador de conjunto de filas del esquema para Foreach de ADO.NET  
  
1.  Cree un administrador de conexiones de ADO.NET que use el proveedor OLE DB para Microsoft ACE para conectarse al libro de Excel. En la página Todos del cuadro de diálogo **Administrador de conexiones**, asegúrese de especificar la versión de Excel (en este caso, Excel 12.0) como valor de la propiedad Propiedades extendidas. Para obtener más información, consulte [agregar, eliminar o compartir un administrador de conexiones en un paquete](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655).  
  
2.  Cree una variable de cadena que recibirá el nombre de la tabla actual en cada iteración del bucle.  
  
3.  Agregue un contenedor de bucles Foreach a la pestaña **Flujo de control** . Para obtener más información sobre cómo configurar el contenedor de bucles Foreach, vea [Configurar un contenedor de bucles Foreach](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25).  
  
4.  En la página **Colección** del **Editor de bucles Foreach**, seleccione el enumerador de conjunto de filas del esquema para Foreach de ADO.NET.  
  
5.  Como valor de **Conexión**, seleccione el administrador de conexiones de ADO.NET que creó previamente.  
  
6.  Como valor de **Esquema**, seleccione Tablas.  
  
    > [!NOTE]  
    >  La lista de tablas de un libro de Excel incluye tanto hojas (que tienen el sufijo $) como rangos con nombre. Si tiene que filtrar la lista para obtener solo las hojas o solo los rangos con nombre, escriba código personalizado en una tarea Script para este fin. Para obtener más información, consulte [trabajar con archivos de Excel con la tarea de secuencia de comandos](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md).  
  
7.  En la página **Asignaciones de variables** , asigne Índice 2 a la variable de cadena que creó antes para albergar el nombre de la tabla actual.  
  
8.  Cierre el **Editor de bucles Foreach**.  
  
9. Cree tareas en el contenedor de bucles Foreach que utilicen el administrador de conexiones con Excel para realizar las mismas operaciones en cada tabla de Excel en el libro especificado. Si usa una tarea Script para examinar el nombre de la tabla enumerada o para trabajar con cada tabla, recuerde agregar la variable de cadena a la propiedad ReadOnlyVariables de la tarea Script.  
  
## <a name="see-also"></a>Ver también  
 [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
 [Configurar un contenedor de bucles Foreach](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)   
 [Agregar o cambiar una expresión de propiedad](../../integration-services/expressions/add-or-change-a-property-expression.md)   
 [Administrador de conexiones de Excel](../../integration-services/connection-manager/excel-connection-manager.md)   
 [Origen de Excel](../../integration-services/data-flow/excel-source.md)   
 [Destino de Excel](../../integration-services/data-flow/excel-destination.md)   
 [Trabajar con archivos de Excel con la tarea Script](../../integration-services/extending-packages-scripting-task-examples/working-with-excel-files-with-the-script-task.md)  
  
  
