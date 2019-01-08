---
title: Cargar datos mediante el destino de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- loading data
- OLE DB destination [Integration Services]
- destinations [Integration Services], OLE DB
ms.assetid: 78899498-725e-4300-a7af-f983f4ea384b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 865ff640cb64fe212afa5ece8bbdaa7f0be4a14c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749517"
---
# <a name="load-data-by-using-the-ole-db-destination"></a>Cargar datos mediante el destino de OLE DB
  Para agregar y configurar un destino de OLE DB, el paquete ya debe incluir al menos una tarea Flujo de datos y un origen.  
  
### <a name="to-load-data-using-an-ole-db-destination"></a>Para cargar datos mediante un destino de OLE DB  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el destino de OLE DB a la superficie de diseño.  
  
4.  Conecte el destino de OLE DB al flujo de datos arrastrando el conector desde un origen de datos o una transformación anterior al destino.  
  
5.  Haga doble clic en el destino de OLE DB.  
  
6.  En el **Editor de destino de OLE DB** , en la página **Administrador de conexiones** , seleccione un administrador de conexiones OLE DB o haga clic en **Nuevo** para crear un nuevo administrador de conexiones. Para más información, consulte [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md).  
  
7.  Seleccione el método de acceso de datos:  
  
    -   **Tabla o vista** Seleccione una tabla o vista en la base de datos que contiene los datos.  
  
    -   **Tabla o vista - carga rápida** seleccione una tabla o vista en la base de datos que contiene los datos y, a continuación, establezca las opciones de carga rápida: **Mantener valores de identidad**, **mantener null**, **bloqueo de tabla**, **restricción Check**, **filas por lote**, o **máximo tamaño de confirmación de inserción**.  
  
    -   **Variable de nombre de tabla o nombre de vista** Seleccione la variable definida por el usuario que contiene el nombre de una tabla o vista en la base de datos.  
  
    -   **Carga rápida de variable de nombre de tabla o nombre de vista** Seleccione la variable definida por el usuario que contiene el nombre de una tabla o vista en la base de datos que contiene los datos y, después, establezca las opciones de carga rápida.  
  
    -   **Comando SQL** Escriba un comando SQL o haga clic en **Generar consulta** para escribir un comando SQL mediante el **Generador de consultas**.  
  
8.  Haga clic en **Asignaciones** y asigne columnas de la lista **Columnas de entrada disponibles** a columnas en la lista **Columnas de destino disponibles** arrastrando columnas de una lista a otra.  
  
    > [!NOTE]  
    >  El destino de OLE DB asigna automáticamente las columnas con el mismo nombre.  
  
9. Para configurar la salida de error, haga clic en **Salida de error**. Para más información, vea [Configurar una salida de error en un componente de flujo de datos](../configure-an-error-output-in-a-data-flow-component.md).  
  
10. Haga clic en **Aceptar**.  
  
11. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Destino de OLE DB](ole-db-destination.md)   
 [Transformaciones de Integration Services](transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](integration-services-paths.md)   
 [Tarea Flujo de datos](../control-flow/data-flow-task.md)  
  
  
