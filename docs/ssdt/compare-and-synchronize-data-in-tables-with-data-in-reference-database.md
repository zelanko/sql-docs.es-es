---
title: Comparación y sincronización de datos de una o más tablas con datos de una base de datos de referencia | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 96d743b0-b69a-45bb-ae0e-62103dca76e2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 23b3057a23737eb43206f9615ce2f83bad6f5610
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745113"
---
# <a name="compare-and-synchronize-data-in-one-or-more-tables-with-data-in-a-reference-database"></a>Comparar y sincronizar datos de una o más tablas con datos de una base de datos de referencia
Puede comparar los datos de una base de datos de *origen* y una base de datos de *destino* y especificar qué tablas se deben comparar. Puede revisarlos y decidir qué cambios sincronizar. A continuación, puede actualizar el destino para sincronizar las bases de datos o exportar el script de actualización al editor de Transact\-SQL o a un archivo.  
  
Por ejemplo, puede sincronizar las bases de datos para actualizar un servidor de ensayo con una copia de los datos de producción. También puede sincronizar una o varias tablas para poblarlas con datos de referencia de otra. Además, puede comparar datos antes y después de ejecutar pruebas como forma adicional de comprobación.  
  
Puede comparar datos en dos bases de datos, pero no puede especificar un archivo de proyecto de base de datos o .dacpac para compararlos porque no contiene datos.  
  
Esta sección contiene los siguientes temas:  
  
-   [Cómo: Comparar y sincronizar los datos de dos bases de datos](../ssdt/how-to-compare-and-synchronize-the-data-of-two-databases.md)  
  
-   [Cómo: Ver diferencias de datos](../ssdt/how-to-view-data-differences.md)  
  
## <a name="requirements"></a>Requisitos  
Cuando se comparan datos de una tabla o vista, la tabla o vista en la base de datos de origen debe compartir varios atributos con una tabla o vista en la base de datos de destino. Las tablas y vistas que no cumplen los siguientes criterios no se comparan y no aparecen en la segunda página del asistente **Nueva comparación de datos**:  
  
-   Las tablas deben tener nombres de columnas coincidentes que tengan tipos de datos compatibles.  
  
    Los nombres de tablas, vistas y propietarios distinguen entre mayúsculas y minúsculas.  
  
-   Las tablas deben tener la misma clave principal, índice único o restricción UNIQUE.  
  
-   Las vistas deben tener los mismos índices clúster únicos.  
  
-   Puede comparar una tabla con una vista solo si tienen el mismo nombre.  
  
Cada objeto tiene una clave o un índice que determina los objetos a los que corresponde. Sin embargo, cada tabla o vista puede tener más de una clave principal, índice único o restricción UNIQUE. Por tanto, debe especificar qué clave, índice o restricción utilizar.  
  
## <a name="common-tasks"></a>Tareas comunes  
En esta sección, puede encontrar descripciones de las tareas comunes que admiten este escenario.  
  
**Establezca las opciones para controlar cómo se comparan los datos:** cuando se comparan datos, puede omitir con seguridad columnas de identidad, deshabilitar desencadenadores y deshabilitar claves externas. También puede quitar claves principales, índices y restricciones UNIQUE del script de actualización.  
  
**Compare los datos de las tablas y actualice opcionalmente el destino para que coincida con el origen:** después de especificar una base de datos de origen y de destino para comparar y ejecutar la comparación, puede ver los resultados en la ventana **Comparación de datos**. Puede ver no solo los detalles de las diferencias sino también del script de actualización que puede utilizar para sincronizar los datos. Después de identificar diferencias entre las dos bases de datos, puede especificar una acción para cada diferencia. A continuación, puede actualizar el destino o exportar el script de actualización al editor de Transact\-SQL o a un archivo. Puede que desee exportar el script para que usted u otra persona pueda revisarlo antes de aplicar los cambios.  
  
## <a name="UnderstandingDataCompareResults"></a>Reconocimiento de los resultados de la comparación  
La tabla siguiente describe las cinco columnas de la ventana **Comparación de datos**.  
  
|columna|Notas|  
|----------|---------|  
|Objeto|Muestra el nombre de la tabla o vista y una casilla que indica si el destino se debe sincronizar al escribir actualizaciones o exportar el script de actualización. La casilla no está disponible para tablas o vistas que no contienen datos.|  
|Varios registros|Muestra el número de registros en el destino con la misma clave pero no los mismos datos que en el origen. Los paréntesis incluyen el número de registros que se marcan para actualizar cuando se escriben actualizaciones o se exporta el script de actualización.|  
|Solo en el origen|Muestra el número de registros en el origen que no se producen en el destino. Los paréntesis incluyen el número de registros que se marcan para agregarlos cuando se escriben actualizaciones o se exporta el script de actualización.|  
|Sólo en destino|Muestra el número de registros en el destino que no se producen en el origen. Los paréntesis incluyen el número de los registros que se marcan para eliminar cuando se escriben actualizaciones o se exporta el script de actualización.|  
|Registros idénticos|Muestra el número de registros en el destino con la misma clave y los mismos datos que en el origen. Estos registros no se actualizan al escribir actualizaciones o exportar el script de actualización.|  
  
### <a name="table-and-view-details"></a>Detalles de las vistas y tablas  
Al hacer clic en cualquier tabla o vista en la ventana **Comparación de datos**, el panel de detalles muestra todas las filas que la tabla o vista contiene. Cada pestaña en el panel de detalles muestra una categoría distinta (Diferentes registros, Solo en origen, Solo en destino, Registros idénticos). Para cada fila, puede activar o desactivar la casilla correspondiente para indicar si desea incluir ese cambio en el script de actualización.  
  
## <a name="see-also"></a>Ver también  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
[Cómo: Usar Comparación de esquemas para comparar distintas definiciones de base de datos](../ssdt/how-to-use-schema-compare-to-compare-different-database-definitions.md)  
  
