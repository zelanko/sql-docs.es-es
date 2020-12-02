---
description: 'Lección 1-7: Adición y configuración del destino de OLE DB'
title: 'Paso 7: Adición y configuración del destino de OLE DB | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 442c841d-d528-4bf0-8724-7156f909ee50
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c30d9c27550913f5c83334ff33ff3a1cc08e1bc
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2020
ms.locfileid: "90990418"
---
# <a name="lesson-1-7-add-and-configure-the-ole-db-destination"></a>Lección 1-7: Adición y configuración del destino de OLE DB

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



Ahora, el paquete puede extraer datos de un origen de archivo plano y transformarlos a un formato compatible con el destino. La tarea siguiente consiste en cargar los datos transformados en el destino. Para cargar los datos, debe agregar un destino de OLE DB al flujo de datos. El destino de OLE DB puede usar una tabla de bases de datos, una vista o un comando SQL para cargar datos en distintas bases de datos compatibles con OLE DB.  
  
En esta tarea, se agrega y configura un destino de OLE DB para usar el administrador de conexiones de OLE DB creado antes.  
  
## <a name="add-and-configure-the-sample-ole-db-destination"></a>Adición y configuración del destino de OLE DB de ejemplo  
  
1.  En el **Cuadro de herramientas de SSIS**, expanda **Otros destinos** y arrastre **Destino de OLE DB** a la superficie de diseño de la pestaña **Flujo de datos** . Coloque el **destino de OLE DB** directamente debajo de la transformación **Lookup Date Key**.  
  
2.  Haga clic en la transformación **Lookup Date Key** y arrastre la flecha de color azul hasta el nuevo **Destino de OLE DB** para conectar los dos componentes entre sí.  
  
3.  En el cuadro de diálogo **Selección de entrada y salida**, haga clic en **Salida de entradas coincidentes de búsqueda** en el cuadro de lista **Salida** y, después, haga clic en **Aceptar**.  
  
4.  En la superficie de diseño **Flujo de datos**, haga clic en el nombre **Destino de OLE DB** en el nuevo componente **Destino de OLE DB** y cambie el nombre por **Sample OLE DB Destination**.  
  
5.  Haga doble clic en **Sample OLE DB Destination**.  
  
6.  En el cuadro de diálogo **Editor de destino de OLE DB**, asegúrese de que **localhost.AdventureWorksDW2012** está seleccionado en el cuadro **Administrador de conexiones OLE DB**.  
  
7.  En el cuadro **Nombre de la tabla o la vista**, escriba o seleccione **[dbo].[FactCurrencyRate]**.  
 
8.  Si ya existe una tabla denominada **NewFactCurrencyRate**, elimínela ahora. Creará la tabla en el paso siguiente.
 
9.  Haga clic en el botón **Nuevo** para crear una tabla.  Cambie el nombre de la tabla en el script de **Sample OLE DB Destination** a **NewFactCurrencyRate**.  Seleccione **Aceptar**.  
 
10. Al hacer clic en **Aceptar**, se cierra el cuadro de diálogo y el **Nombre de la tabla o la vista** cambia automáticamente a **NewFactCurrencyRate**.  
  
11. Haga clic en **Asignaciones**.  
  
12. Compruebe que las columnas de entrada **AverageRate**, **CurrencyKey**, **EndOfDayRate** y **DateKey** están correctamente asignadas a las columnas de destino. Si hay columnas con el mismo nombre asignadas, la asignación es correcta.  
  
13. Seleccione **Aceptar**.  
  
14. Haga clic con el botón derecho en **Sample OLE DB Destination** y seleccione **Propiedades**.  
  
15. En la ventana **Propiedades**, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos)** y la propiedad **DefaultCodePage** en **1252**.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 8: Anotación y formato del paquete de la lección 1](../integration-services/lesson-1-8-making-the-lesson-1-package-easier-to-understand.md)  
  
## <a name="see-also"></a>Vea también  
[Destino de OLE DB](../integration-services/data-flow/ole-db-destination.md)  
  
  
  
