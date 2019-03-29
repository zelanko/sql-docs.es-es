---
title: Destino de Excel | Microsoft Docs
ms.custom: ''
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.exceldest.f1
- sql13.dts.designer.exceldestadapter.connection.f1
- sql13.dts.designer.exceldestadapter.mappings.f1
- sql13.dts.designer.exceldestadapter.erroroutput.f1
helpviewer_keywords:
- destinations [Integration Services], Excel
- Excel [Integration Services]
ms.assetid: 37c07446-1264-4814-b4f5-9c66d333bb24
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ab8a7da7e45d9d623fd436ac3b6c0e8b3d945536
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289831"
---
# <a name="excel-destination"></a>Destino de Excel
  El destino de Excel carga datos en hojas de cálculo o rangos en libros de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel.  

> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).
  
## <a name="access-modes"></a>Modos de acceso  
 El destino de Excel proporciona tres modos diferentes de acceso a los datos para cargar datos:  
  
-   Una tabla o vista.  
  
-   Una tabla o vista especificadas en una variable.  
  
-   Los resultados de una instrucción SQL. La consulta puede tener parámetros.  
  
## <a name="configure-the-excel-destination"></a>Configurar el destino de Excel  
 El destino de Excel usa un administrador de conexiones de Excel para conectarse a un origen de datos, y el administrador de conexiones especifica el archivo de libro que se debe usar. Para más información, consulte [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
 El destino de Excel tiene una entrada normal y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica todas las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de Excel](../../integration-services/data-flow/excel-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="excel-destination-editor-connection-manager-page"></a>Editor de destino de Excel (página Administrador de conexiones)
  Utilice la página **Administrador de conexiones** del cuadro de diálogo **Editor de destino de Excel** para especificar la información de orígenes de datos y para obtener una vista previa de los resultados. El destino de Excel carga los datos en una hoja de cálculo o en un rango con nombre de un libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] .  
  
> [!NOTE]  
>  La propiedad **CommandTimeout** del destino de Excel no está disponible en el **Editor de destino de Excel**, pero se puede establecer mediante el **Editor avanzado**. Además, ciertas opciones de carga rápida solo están disponibles en el **Editor avanzado**. Para obtener más información acerca de estas propiedades, vea la sección sobre el destino de Excel en [Excel Custom Properties](../../integration-services/data-flow/excel-custom-properties.md).  
  
### <a name="static-options"></a>Opciones estáticas  
 **Administrador de conexiones con Excel**  
 Seleccione un Administrador de conexiones con Excel en la lista o cree una conexión haciendo clic en **Nueva**.  
  
 **Nueva**  
 Cree un administrador de conexiones mediante el cuadro de diálogo **Administrador de conexiones con Excel** .  
  
 **Modo de acceso a datos**  
 Especifique el método para seleccionar datos del origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tabla o vista|Carga datos en una hoja de cálculo o en un rango con nombre del origen de datos de Excel.|  
|Variable de nombre de tabla o nombre de vista|Especifique la hoja de calculo o el rango con nombre de una variable.<br /><br /> **Información relacionada**: [Usar variables en paquetes](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Cargue datos en el destino de Excel utilizando una consulta SQL.|  
  
 **Nombre de la hoja de Excel**  
 Seleccione el destino de Excel de la lista desplegable. Si la lista está vacía, haga clic en **Nuevo**.  
  
 **Nueva**  
 Haga clic en **Nuevo** para iniciar el cuadro de diálogo **Crear tabla** . Al hacer clic en **Aceptar**, el cuadro de diálogo crea el archivo de Excel al que señala el **Administrador de conexiones con Excel** .  
  
 **Datos existentes de la vista**  
 Obtenga una vista previa de los resultados mediante el cuadro de diálogo **Vista previa de los resultados de la consulta** . La vista previa puede mostrar hasta 200 filas.  
  
### <a name="data-access-mode-dynamic-options"></a>Opciones dinámicas del modo de acceso a datos  
  
#### <a name="data-access-mode--table-or-view"></a>Modo de acceso a datos = Tabla o vista  
 **Nombre de la hoja de Excel**  
 Seleccione el nombre de la hoja de cálculo o el rango con nombre de los disponibles en el origen de datos.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modo de acceso a datos = Variable de nombre de tabla o nombre de vista  
 **Nombre de variable**  
 Seleccione la variable que contiene el nombre de la hoja de cálculo o el rango con nombre.  
  
#### <a name="data-access-mode--sql-command"></a>Modo de acceso a datos = Comando SQL  
 **Texto de comando SQL**  
 Escriba el texto de una consulta SQL, genere la consulta haciendo clic en **Generar consulta**, o bien busque el archivo que contiene el texto de la consulta haciendo clic en **Examinar**.  
  
 **Generar consulta**  
 Use el cuadro de diálogo **Generador de consultas** para crear visualmente la consulta SQL.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para buscar el archivo que contiene el texto de la consulta SQL.  
  
 **Analizar consulta**  
 Comprueba la sintaxis del texto de la consulta.  
  
## <a name="excel-destination-editor-mappings-page"></a>Editor de destino de Excel (página Asignaciones)
  Utilice la página **Asignaciones** del cuadro de diálogo **Editor de destino de Excel** para asignar columnas de entrada a columnas de destino.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Muestra la lista de columnas de entrada disponibles. Utilice una operación de arrastrar y colocar para asignar columnas de entrada disponibles de la tabla a columnas de destino.  
  
 **Columnas de destino disponibles**  
 Muestra la lista de columnas de destino disponibles. Utilice una operación de arrastrar y colocar para asignar columnas de destino disponibles de la tabla a columnas de entrada.  
  
 **Columna de entrada**  
 Muestra las columnas de entrada seleccionadas de la tabla anterior. Puede cambiar las asignaciones utilizando la lista de **Columnas de entrada disponibles**.  
  
 **Columna de destino**  
 Muestra las columnas de destino disponibles, independientemente de si están asignadas o no.  
  
## <a name="excel-destination-editor-error-output-page"></a>Editor de destino de Excel (página Salida de error)
  Utilice la página **Avanzadas** del cuadro de diálogo **Editor de destino de Excel** para especificar opciones para el control de errores.  
  
### <a name="options"></a>Opciones  
 **Entrada o salida**  
 Muestra el nombre del origen de datos.  
  
 **Columna**  
 Muestra las columnas externas (de origen) seleccionadas en el nodo **Administrador de conexiones** del cuadro de diálogo **Editor de origen de Excel**.  
  
 **Error**  
 Permite especificar qué debe ocurrir cuando se produce un error: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Temas relacionados:** [Control de errores en los datos](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Truncamiento**  
 Permite especificar qué debe ocurrir cuando se produce un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Descripción**  
 Muestra la descripción del error.  
  
 **Establecer este valor en las celdas seleccionadas**  
 Permite especificar qué debe ocurrir en todas las celdas seleccionadas cuando se produce un error o un truncamiento: omitir el error, redirigir la fila o hacer que el componente no funcione.  
  
 **Aplicar**  
 Aplica la opción de control de errores a las celdas seleccionadas.  
  
## <a name="see-also"></a>Consulte también  
 [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
 [Origen de Excel](../../integration-services/data-flow/excel-source.md)   
[Administrador de conexiones de Excel](../connection-manager/excel-connection-manager.md)
