---
title: "Implementar una búsqueda en modo No hay caché o Caché parcial | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- Lookup transformation
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: 01b7fbca-5181-4d47-9f75-7f25af6b40d2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4312836f421788df8a2927afc8f6e0986a0490d2
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="implement-a-lookup-in-no-cache-or-partial-cache-mode"></a>Implementar una búsqueda en modo No hay caché o Caché parcial
  Puede configurar la transformación Búsqueda para utilizar el modo Caché parcial o el modo Sin caché:  
  
-   Caché parcial  
  
     Las filas con entradas coincidentes en el conjunto de datos de referencia y, opcionalmente, las que no tienen entradas coincidentes se almacenan en la memoria caché. Cuando se supera el tamaño de la memoria caché, la transformación Búsqueda quita automáticamente de la memoria caché las filas utilizadas con menor frecuencia.  
  
-   Sin caché  
  
     No se carga ningún dato en la caché.  
  
 Tanto si se selecciona el modo Caché parcial como el modo Sin caché, se utiliza un administrador de conexiones OLE DB para conectar con el conjunto de datos de referencia. El conjunto de datos de referencia se genera mediante una tabla, vista o consulta SQL durante la ejecución de la transformación Búsqueda  
  
### <a name="to-implement-a-lookup-transformation-in-no-cache-or-partial-cache-mode"></a>Para implementar una transformación Búsqueda en modo No hay caché o Caché parcial  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete con el que desea trabajar y ábralo.  
  
2.  En la pestaña **Flujo de datos** , agregue una transformación de Búsqueda.  
  
3.  Conecte la transformación Búsqueda al flujo de datos arrastrando un conector desde un origen o una transformación anterior hasta la transformación Búsqueda.  
  
    > [!NOTE]  
    >  Una transformación Búsqueda que se configure para utilizar el modo sin memoria caché podría no validarse si esa transformación se conectara a un archivo plano que contuviera un campo de fecha vacío. El que la transformación se valide depende de si el administrador de conexiones para el archivo plano se ha configurado para conservar los valores NULL. Para asegurarse de que la transformación Búsqueda se valida, en el **Editor de origen de archivos planos**, de la página **Administrador de conexiones**, seleccione la opción **Conservar los valores null del origen como valores null en el flujo de datos** .  
  
4.  Haga doble clic en el origen o la transformación anterior para configurar el componente.  
  
5.  Haga doble clic en la transformación Búsqueda y, luego, en el **Editor de transformación Búsqueda**, en la página **General** , seleccione **Caché parcial** o **No hay caché**.  
  
6.  En la lista **Especificar cómo administrar las filas con entradas no coincidentes** , seleccione una opción de control de errores.  
  
7.  En la página **Conexión** , seleccione un administrador de conexiones en la lista **Administradores de conexión OLE DB** o haga clic en **Nuevo** para crear un nuevo administrador de conexiones. Para más información, consulte [OLE DB Connection Manager](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
8.  Realice uno de los pasos siguientes:  
  
    -   Haga clic en **Usar una tabla o una vista**y, a continuación, seleccione una tabla o una vista, o haga clic en **Nueva** para crear una tabla o una vista.  
  
    -   Haga clic en **Usar los resultados de una consulta SQL**y, a continuación, genere una consulta en la ventana **Comando SQL** .  
  
         O bien  
  
         Haga clic en **Generar consulta** para generar una consulta con las herramientas gráficas que proporciona el **Generador de consultas** .  
  
         O bien  
  
         Haga clic en **Examinar** para importar una instrucción SQL de un archivo.  
  
     Para validar la consulta SQL, haga clic en **Analizar consulta**.  
  
     Para ver un ejemplo de los datos, haga clic en **Vista previa**.  
  
9. Haga clic en la página **Columnas** y, a continuación, arrastre por lo menos una columna desde la lista **Columnas de entrada disponibles** hasta una columna de la lista **Columnas de búsqueda disponibles** .  
  
    > [!NOTE]  
    >  La transformación Búsqueda asigna automáticamente las columnas que tienen el mismo nombre y el mismo tipo de datos.  
  
    > [!NOTE]  
    >  Las columnas deben tener tipos coincidentes de datos para asignarse. Para obtener más información, vea [Integration Services Data Types](../../../integration-services/data-flow/integration-services-data-types.md).  
  
10. Incluir las columnas de búsqueda en el resultado realizando los pasos siguientes:  
  
    1.  En la lista **Columnas de búsqueda disponibles** , seleccione las columnas.  
  
    2.  En la lista **Operación de búsqueda** , especifique si los valores de las columnas de búsqueda reemplazan los valores de la columna de entrada o se escriben en una nueva columna.  
  
11. Si seleccionó **Caché parcial** en el paso 5, en la página **Avanzadas** , establezca las opciones de caché siguientes:  
  
    -   En la lista **Tamaño de caché (32 bits)** , seleccione el tamaño de caché para los entornos de 32 bits.  
  
    -   En la lista **Tamaño de caché (64 bits)** , seleccione el tamaño de caché para los entornos de 64 bits.  
  
    -   Para almacenar en memoria caché las filas con entradas no coincidentes en la referencia, seleccione **Habilitar caché para las filas con entradas no coincidentes**.  
  
    -   En la lista **Asignación desde caché** , seleccione el porcentaje que debe utilizarse de la memoria caché para almacenar las filas sin entradas coincidentes.  
  
12. Para modificar la instrucción SQL que genera el conjunto de datos de referencia, seleccione **Modificar la instrucción SQL**y cambie la instrucción SQL mostrada en el cuadro de texto.  
  
     Si la instrucción incluye parámetros, haga clic en **Parámetros** para asignar los parámetros a las columnas de entrada.  
  
    > [!NOTE]  
    >  La instrucción SQL opcional que se especifica en esta página invalida y reemplaza el nombre de tabla que se especificó en la página **Conexión** del **Editor de transformación Búsqueda**.  
  
13. Para configurar la salida de errores, haga clic en la página **Salida de error** y establezca las opciones de control de errores. Para obtener más información, vea [Editor de transformación Búsqueda &#40;página Salida de error&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).  
  
14. Haga clic en **Aceptar** para guardar los cambios en la transformación Búsqueda y, a continuación, ejecute el paquete.  
  
## <a name="see-also"></a>Ver también  
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
