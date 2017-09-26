---
title: 'Paso 7: Agregar y configurar el destino de OLE DB | Documentos de Microsoft'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e50d2f6d1622cc124cf8b55fbd1ae14811d5cc9c
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-7---adding-and-configuring-the-ole-db-destination"></a>Lección 1-7: agregar y configurar el destino de OLE DB
Ahora, el paquete puede extraer datos de un origen de archivo plano y transformar dichos datos en un formato compatible con el destino. La tarea siguiente consiste realmente en cargar los datos transformados en el destino. Para cargar los datos, debe agregar un destino de OLE DB al flujo de datos. El destino de OLE DB puede utilizar una tabla de bases de datos, una vista o un comando SQL para cargar datos en distintas bases de datos compatibles con OLE DB.  
  
En este procedimiento, se agrega y configura un destino de OLE DB para utilizar el administrador de conexiones de OLE DB creado con anterioridad.  
  
### <a name="to-add-and-configure-the-sample-ole-db-destination"></a>Para agregar y configurar un destino de OLE DB de ejemplo  
  
1.  En el **Cuadro de herramientas de SSIS**, expanda **Otros destinos**y arrastre **Destino de OLE DB** a la superficie de diseño de la pestaña **Flujo de datos** . Coloque el destino de OLE DB directamente debajo de la transformación **Lookup Date Key** .  
  
2.  Haga clic en la transformación **Lookup Date Key** y arrastre la flecha verde hasta el **Destino de OLE DB** que acaba de agregar para conectar los dos componentes entre sí.  
  
3.  En el cuadro de diálogo **Selección de entrada y salida** , en el cuadro de lista **Salida** , haga clic en **Salida de entradas coincidentes de búsqueda**y, después, haga clic en **Aceptar**.  
  
4.  En la superficie de diseño **Flujo de datos** , haga clic en **Destino de OLE DB** en el componente **Destino de OLE DB** que acaba de agregar y cambie el nombre por **Sample OLE DB Destination**.  
  
5.  Haga doble clic en **Sample OLE DB Destination**.  
  
6.  En el cuadro de diálogo **Editor de destino de OLE DB** , asegúrese de que **localhost.AdventureWorksDW2012** está seleccionado en el cuadro **Administrador de conexiones OLE DB** .  
  
7.  En el cuadro **Nombre de la tabla o la vista** , escriba o seleccione **[dbo].[FactCurrencyRate]**.  
  
8.  Haga clic en el botón **Nuevo** para crear una nueva tabla.  Cambie el nombre de la tabla en el script a **NewFactCurrencyRate**.  Haga clic en **Aceptar**.  
  
9. Al hacer clic en **Aceptar**, se cerrará el cuadro de diálogo y el **Nombre de la tabla o la vista** cambiará automáticamente a **NewFactCurrencyRate**.  
  
10. Haga clic en **Asignaciones**.  
  
11. Compruebe que las columnas de entrada **AverageRate**, **CurrencyKey**, **EndOfDayRate**y **DateKey** están correctamente asignadas a las columnas de destino. Si hay columnas con el mismo nombre asignadas, la asignación es correcta.  
  
12. Haga clic en **Aceptar**.  
  
13. Haga clic con el botón derecho en **Sample OLE DB Destination** y haga clic en **Propiedades**.  
  
14. En la ventana Propiedades, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos)** y la propiedad**DefaultCodePage** en **1252**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Paso 8: Facilitar la comprensión del paquete de la lección 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>Vea también  
[Destino de OLE DB](../integration-services/data-flow/ole-db-destination.md)  
  
  
  

