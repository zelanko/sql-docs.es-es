---
title: Extraer datos mediante el origen de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- extracting data [Integration Services]
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: 4ca6eeb5-b60e-4b81-86dd-0674be8ae8d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9ca00dfe612f5735f767d50c66ebbb0e079bc39c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432182"
---
# <a name="extract-data-by-using-the-ole-db-source"></a>Extraer datos mediante el origen de OLE DB
  Para agregar y configurar un origen de OLE DB, el paquete ya debe incluir por lo menos una tarea Flujo de datos.  
  
### <a name="to-extract-data-using-an-ole-db-source"></a>Para extraer datos mediante un Origen de OLE DB  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el origen de OLE DB hasta la superficie de diseño.  
  
4.  Haga doble clic en el origen de OLE DB.  
  
5.  En el **Editor de origen de OLE DB** , en la página **Administrador de conexiones** , seleccione un administrador de conexiones OLE DB o haga clic en **Nuevo** para crear un nuevo administrador de conexiones. Para más información, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
6.  Seleccione el método de acceso de datos:  
  
    -   **Tabla o vista** Seleccione una tabla o vista en la base de datos a la que se conecta el administrador de conexiones OLE DB.  
  
    -   **Variable de nombre de tabla o nombre de vista** Seleccione la variable definida por el usuario que contiene el nombre de una tabla o vista en la base de datos a la que se conecta el administrador de conexiones OLE DB.  
  
    -   **Comando SQL** Escriba un comando SQL o haga clic en **Generar consulta** para escribir un comando SQL mediante el **Generador de consultas**.  
  
        > [!NOTE]  
        >  El comando puede incluir parámetros. Para obtener más información, vea [Asignar parámetros de consulta a variables en un componente de flujo de datos](map-query-parameters-to-variables-in-a-data-flow-component.md).  
  
    -   **Comando SQL de variable** Seleccione la variable definida por el usuario que contiene el comando SQL.  
  
        > [!NOTE]  
        >  Las variables se deben definir en el ámbito de la misma tarea Flujo de datos que contiene el origen OLE DB, o en el ámbito del mismo paquete. Además, la variable debe tener un tipo de datos de cadena.  
  
7.  Para actualizar la asignación entre las columnas externas y de salida, haga clic en **Columnas** y seleccione diferentes columnas en la lista **Columna externa** .  
  
8.  Opcionalmente, actualice los nombres de las columnas de salida modificando los valores en la lista **Columna de salida** .  
  
9. Para configurar la salida de error, haga clic en **Salida de error**. Para más información, vea [Configurar una salida de error en un componente de flujo de datos](../configure-an-error-output-in-a-data-flow-component.md).  
  
10. Puede hacer clic en **Vista previa** para ver hasta 200 filas de los datos extraídos por el origen de OLE DB.  
  
11. Haga clic en **OK**.  
  
12. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Origen de OLE DB](ole-db-source.md)   
 [Transformaciones de Integration Services](transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](integration-services-paths.md)   
 [Tarea Flujo de datos](../control-flow/data-flow-task.md)  
  
  
