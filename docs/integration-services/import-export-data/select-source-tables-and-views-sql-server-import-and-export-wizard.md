---
title: Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.selectsourcetablesandviews.f1
ms.assetid: f60e1a19-2ea6-403c-89ab-3e60ac533ea0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e20ae3e7392c01195ecb8cb829976efb3d6ad2c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723736"
---
# <a name="select-source-tables-and-views-sql-server-import-and-export-wizard"></a>Seleccionar tablas y vistas de origen (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de especificar que quiere copiar una tabla completa o después de proporcionar una consulta, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Seleccionar tablas y vistas de origen**. En esta página, seleccione las tablas y vistas que quiera copiar. A continuación, asigne las tablas de origen a las tablas de destino nuevas o existentes. Opcionalmente, revise la asignación de columnas individuales y obtenga una vista previa de los datos de ejemplo.

> [!TIP]
> Si tiene que copiar más de una base de datos u objetos de base de datos de SQL Server que no sean tablas y vistas, use el Asistente para copiar bases de datos en lugar del Asistente para importación y exportación. Para más información, vea [Usar el Asistente para copiar bases de datos](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="screen-shot---if-youre-going-to-copy-tables"></a>Captura de pantalla: si va a copiar tablas  
 En la siguiente captura de pantalla se muestra un ejemplo de la página **Seleccionar tablas y vistas de origen** del asistente después de seleccionar la opción **Copiar los datos de una o varias tablas o vistas** en la página **Especificar copia de tabla o consulta**. En la lista, se ven todas las tablas y vistas disponibles del origen de datos.
 
En este ejemplo, la lista **Origen** contiene todas las tablas de la base de datos de ejemplo AdventureWorks. La fila seleccionada muestra que el usuario quiere copiar la tabla **Sales.Customer** del origen en la nueva tabla **Sales.CustomerNew** del destino. 
   
 ![Página Seleccionar tablas del Asistente para importación y exportación](../../integration-services/import-export-data/media/select-tables1.png "Página Seleccionar tablas del Asistente para importación y exportación")
  
## <a name="screen-shot---if-you-provided-a-query"></a>Captura de pantalla: si proporcionó una consulta  
 La siguiente captura de pantalla muestra un ejemplo de la página **Seleccionar tablas y vistas de origen** del asistente después de seleccionar la opción **Escribir una consulta para especificar los datos que se van a transferir** en la página **Especificar copia de tabla o consulta**. La lista **Origen** contiene solo una fila, en la cual el elemento denominado `[Query]` representa la consulta que proporcionó en la página **Proporcionar una consulta de origen**.
 
En este ejemplo, el usuario quiere copiar los resultados de la consulta del origen en la tabla **Sales.CustomerNew** del destino.  
    
 ![Página Seleccionar tablas del Asistente para importación y exportación](../../integration-services/import-export-data/media/select-tables2.png "Página Seleccionar tablas del Asistente para importación y exportación")  

## <a name="select-source-and-destination-tables"></a>Seleccionar tablas de destino y origen 
**Source**  
Utilice las casillas para seleccionar en la lista las tablas y vistas disponibles que deben copiarse en el destino. De forma predeterminada, los datos del origen de datos se copian sin cambios. Si crea una tabla de destino nueva, el esquema para la nueva tabla (es decir, la lista de columnas y sus propiedades) también se copia sin cambios desde el origen de datos.

Si proporcionó una consulta, la lista contiene un solo elemento con el nombre `[Query]`. 

**Destino**  
 Seleccione una tabla de destino de la lista para cada tabla o consulta de origen, o escriba el nombre de una nueva tabla que quiera que cree el asistente. Si selecciona una tabla de destino existente, esta debe tener columnas con tipos de datos que sean compatibles con los datos de origen.  

> [!NOTE]
> Si detiene el asistente en este punto para crear una tabla de forma manual en la base de datos de destino con una herramienta externa (como  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]), la nueva tabla no será visible de forma inmediata en la lista de tablas de destino disponibles. Para actualizar la lista de tablas de destino, retroceda hasta la página **Seleccionar un destino** , vuelva a seleccionar la base de datos de destino para actualizar la lista de tablas y vistas disponibles y luego regrese a la página **Seleccionar tablas y vistas de origen** .  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Revisión de las asignaciones de columnas y obtención de una vista previa de los datos (opcional)
**Editar asignaciones**   
Si quiere, puede hacer clic en **Editar asignaciones** para ver el cuadro de diálogo **Asignaciones de columnas** de la tabla seleccionada. Use el cuadro de diálogo **Asignaciones de columnas** para hacer lo siguiente:
-   Revise la asignación de columnas individuales entre el origen y el destino.
-   Copie solo un subconjunto de columnas si selecciona **Omitir** para las columnas que no desea copiar.

Para más información, vea [Asignaciones de columnas](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Vista previa**  
Si quiere, puede hacer clic en **Vista previa** para obtener una vista previa de hasta 200 filas de datos de ejemplo en el cuadro de diálogo **Vista previa de los datos**. Esto confirma que el asistente va a copiar los datos que quiere copiar. Para más información, vea [Vista previa de los datos](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Después de obtener una vista previa de los datos, es posible que quiera cambiar las opciones que seleccionó en páginas anteriores del asistente. Para realizar estas modificaciones, vuelva a la página **Seleccionar tablas y vistas de origen** y después haga clic en **Atrás** para volver a las páginas anteriores en las que puede cambiar sus selecciones.  

## <a name="select-source-and-destination-tables-for-excel"></a>Seleccionar tablas de destino y origen para Excel

> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

### <a name="excel-source-tables"></a>Tablas de origen de Excel
En la lista de vistas y tablas de origen para un origen de datos de Excel se incluyen dos tipos de objetos de Excel.
-   **Hojas de cálculo.** Los nombres de las hojas de cálculo van seguidos del signo de dólar ($) (por ejemplo, **"Hoja1$"** ).
-   **Rangos con nombre.** Los rangos con nombre, si los hay, se enumeran por nombre.

Si quiere cargar datos desde un intervalo de celdas específico y sin nombre (por ejemplo, **[Hoja1$A1:B4]** ) o con destino a ese intervalo, tendrá que escribir una consulta. Vuelva a la página **Especificar copia de tabla o consulta** y seleccione **Escribir una consulta para especificar los datos que se van a transferir**.

### <a name="excel-destination-tables"></a>Tablas de destino de Excel
Si va a exportar datos a Excel, puede especificar el destino de una de las tres formas siguientes.
-   **Hoja de cálculo.** Para especificar una hoja de cálculo, anexe el carácter $ al final del nombre de la hoja y agregue delimitadores alrededor de la cadena (por ejemplo, **[Hoja1$]** ).
-   **Rango con nombre.** Para especificar un rango con nombre, use simplemente el nombre del rango (por ejemplo, **MiRangoDeDatos**).
-   **Rango sin nombre.** Para especificar un rango de celdas al que no ha asignado un nombre, anexe el carácter $ al final del nombre de la hoja, agregue la especificación del rango y agregue delimitadores alrededor de la cadena (por ejemplo, **[Hoja1$A1:B4]** ).

> [!TIP]
> Si usa Excel como origen o destino, es una buena idea hacer clic en **Editar asignaciones** y revisar las asignaciones de tipos de datos de la página **Asignaciones de columnas** . 

## <a name="whats-next"></a>¿Qué sigue?  
 Después de seleccionar las tablas y vistas existentes que quiere copiar y de asignarlas a sus destinos, la página siguiente es **Guardar y ejecutar el paquete**. En esta página, especifique si quiere ejecutar la operación de copia inmediatamente. Según la configuración, también puede guardar el paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creado por el asistente para personalizarlo y volver a usarlo más adelante. Para más información, vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
 ## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)



