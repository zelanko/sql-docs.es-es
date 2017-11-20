---
title: Carga masiva de datos mediante el destino de SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: 8f982f85-a82e-4e2d-9cd8-cd2f85402d8e
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6592de5c7bd0ca674c797d2d3e28f3adbe7dd339
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="bulk-load-data-by-using-the-sql-server-destination"></a>Realizar una carga masiva de datos mediante el destino de SQL Server
  Para agregar y configurar un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen de datos.  
  
### <a name="to-load-data-using-a-sql-server-destination"></a>Para cargar datos mediante un destino de SQL Server  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la superficie de diseño.  
  
4.  Conecte el destino a un origen o a una transformación previa en el flujo de datos arrastrando un conector al destino.  
  
5.  Haga doble clic en el destino.  
  
6.  En el **Editor de destino de SQL Server**, en la página del **Administrador de conexiones** , seleccione un administrador de conexiones OLE DB o haga clic en **Nuevo** para crear un nuevo administrador de conexiones. Para más información, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Para especificar la tabla o vista en la que desea cargar los datos, realice una de las siguientes acciones:  
  
    -   Seleccione una tabla o vista existente.  
  
    -   Haga clic en **Nuevo**y, en el cuadro de diálogo **Crear tabla** , escriba una instrucción SQL que cree una tabla o vista.  
  
        > [!NOTE]  
        >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera una instrucción CREATE TABLE predeterminada basada en el origen de datos conectado. La instrucción predeterminada CREATE TABLE no incluirá el atributo FILESTREAM, aunque la tabla de origen tenga una columna con el atributo FILESTREAM declarado. Para ejecutar un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con el atributo FILESTREAM, implemente en primer lugar el almacenamiento de FILESTREAM en la base de datos de destino. A continuación, agregue el atributo FILESTREAM a la instrucción CREATE TABLE en el cuadro de diálogo **Crear tabla** . Para obtener más información, vea [Datos de objeto binario grande &#40;Blob&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
8.  Haga clic en **Asignaciones** y asigne columnas de la lista **Columnas de entrada disponibles** a columnas en la lista **Columnas de destino disponibles** arrastrando columnas de una lista a otra.  
  
    > [!NOTE]  
    >  El destino asigna automáticamente las columnas con el mismo nombre.  
  
9. Haga clic en **Avanzadas** y establezca las opciones de carga masiva: **Mantener valores de identidad**, **Mantener valores NULL**, **Bloqueo de tabla**, **Comprobar restricciones**y **Activar desencadenadores**.  
  
     Opcionalmente, especifique la primera y última fila de entrada que desea insertar, la cantidad máxima de errores que pueden producirse antes de que se detenga la operación de inserción y las columnas en las que se ordena la inserción.  
  
    > [!NOTE]  
    >  El orden es determinado por el orden en que se enumeran las columnas.  
  
10. Haga clic en **Aceptar**.  
  
11. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados** , en el menú **Archivo** .  
  
## <a name="see-also"></a>Vea también  
 [Destino de SQL Server](../../integration-services/data-flow/sql-server-destination.md)   
 [Transformaciones de Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](../../integration-services/data-flow/integration-services-paths.md)   
 [Tarea flujo de datos](../../integration-services/control-flow/data-flow-task.md)  
  
  

