---
title: Cargar datos mediante el destino de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 339ec0a8-922e-48c0-97b3-fc5ee34f95e3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 733e6c8000f3a14127b0f3a8704b43af81fa0f85
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292328"
---
# <a name="load-data-by-using-the-odbc-destination"></a>Cargar datos mediante el destino de ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Este procedimiento muestra cómo cargar datos mediante el destino ODBC. Para agregar y configurar un destino ODBC el paquete ya debe incluir al menos una tarea Flujo de datos y un origen.  
  
### <a name="to-load-data-using-an-odbc-destination"></a>Para cargar datos mediante un destino ODBC  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que desee.  
  
2.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el destino ODBC a la superficie de diseño.  
  
3.  Arrastre una salida disponible de un componente de flujo de datos a la entrada del destino ODBC.  
  
4.  Haga doble clic en el destino ODBC.  
  
5.  En el **Editor de destino ODBC** , en la página **Administrador de conexiones** , seleccione un administrador de conexiones ODBC o haga clic en **Nuevo** para crear un nuevo administrador de conexiones.  
  
6.  Seleccione el método de acceso de datos.  
  
    -   **Nombre de la tabla: Lote** Seleccione esta opción para configurar el destino de ODBC de manera que funcione en modo por lotes. Al seleccionar esta opción, puede establecer el **Tamaño de lote**.  
  
    -   **Nombre de la tabla: Fila a fila**: Seleccione esta opción para configurar el destino de ODBC de manera que se inserte cada una de las filas en la tabla de destino de una en una. Al seleccionar esta opción, los datos se cargan en la tabla una fila cada vez.  
  
7.  En el campo **Nombre de la tabla o la vista** , seleccione una tabla o vista disponible desde la base de datos de la lista o escriba una expresión regular para identificar la tabla. Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el comodín (*) para escribir cualquier parte del nombre con el fin de mostrar la tabla o las tablas que desea usar.  
  
8.  Puede hacer clic en **Vista previa** para ver hasta 200 filas de datos de la tabla seleccionada en el destino ODBC.  
  
9. Haga clic en **Asignaciones** y asigne columnas de la lista **Columnas de entrada disponibles** a columnas en la lista **Columnas de destino disponibles** arrastrando columnas de una lista a otra.  
  
10. Para configurar la salida de error, haga clic en **Salida de error**.  
  
11. Haga clic en **Aceptar**.  
  
12. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Editor de destino de ODBC &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)   
 [Editor de destino de ODBC &#40;página Asignaciones&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)   
 [Editor de orígenes ODBC &#40;página Salida de error&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md)  
  
  
