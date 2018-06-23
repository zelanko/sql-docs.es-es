---
title: Extraer datos mediante el origen de ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 10f25703-49a2-4d45-abab-6b4da2a57ba5
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 7903ff16c9a7f16eca47be37adcefe35cfcb3aec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36196506"
---
# <a name="extract-data-by-using-the-odbc-source"></a>Extraer datos mediante el origen de ODBC
  Este procedimiento describe cómo extraer datos mediante un origen ODBC. Para agregar y configurar un origen ODBC, el paquete ya debe incluir por lo menos una tarea Flujo de datos.  
  
### <a name="to-extract-data-using-an-odbc-source"></a>Para extraer datos mediante un origen ODBC  
  
1.  En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra el paquete de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que desee.  
  
2.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **cuadro de herramientas**, arrastre el origen ODBC a la superficie de diseño.  
  
3.  Haga doble clic en el origen ODBC.  
  
4.  En el cuadro de diálogo **Editor de origen ODBC** , en la página **Administrador de conexiones** , seleccione un administrador de conexiones ODBC o haga clic en **Nuevo** para crear un nuevo administrador de conexiones.  
  
5.  Seleccione el método de acceso de datos.  
  
    -   **Nombre de la tabla**: seleccione una tabla o vista en la base de datos o escriba una expresión regular para identificar la tabla con la que el administrador de conexiones ODBC se conecta.  
  
         Esta lista contiene solo las 1000 primeras tablas. Si la base de datos contiene más de 1000 tablas, puede escribir el principio de un nombre de tabla o usar el comodín (*) para escribir cualquier parte del nombre con el fin de mostrar la tabla o las tablas que desea usar.  
  
    -   **Comando SQL**: escriba un comando SQL o haga clic en **Examinar** para cargar la consulta SQL desde un archivo de texto.  
  
6.  Puede hacer clic en **Vista previa** para ver hasta 200 filas de los datos extraídos por el origen ODBC.  
  
7.  Para actualizar la asignación entre las columnas externas y de salida, haga clic en **Columnas** y seleccione diferentes columnas en la lista **Columna externa** .  
  
8.  Si es necesario actualice los nombres de las columnas de salida modificando los valores en la lista **Columna de salida** .  
  
9. Para configurar la salida de error, haga clic en **Salida de error**.  
  
10. Haga clic en **Aceptar**.  
  
11. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Vea también  
 [Editor de origen ODBC &#40;página Administrador de conexiones&#41;](../odbc-source-editor-connection-manager-page.md)   
 [Editor de orígenes ODBC &#40;página Columnas&#41;](../odbc-source-editor-columns-page.md)   
 [Editor de origen ODBC &#40;página de salida de Error&#41;](../odbc-source-editor-error-output-page.md)  
  
  