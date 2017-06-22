---
title: "Cuadro de diálogo Índices espaciales (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.spatialindexes
ms.assetid: 4d84239a-68c7-4aa2-8602-2b51dd07260f
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5114c8b5fba96020c07758e8c0143c33540a8ad5
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="spatial-indexes-dialog-box-visual-database-tools"></a>Cuadro de diálogo Índices espaciales (Visual Database Tools)
Use el cuadro de diálogo **Índices espaciales** para crear índices para las columnas del tipo de datos **geometry** o **geography** (*columnas espaciales*) que no pueden indizarse mediante el cuadro de diálogo **Índice y claves**. Cada columna espacial puede tener más de un índice espacial, pero se deben crear de uno en uno.  
  
Para más información sobre las restricciones de la creación de índices espaciales, consulte [Información general sobre los índices espaciales](http://msdn.microsoft.com/en-us/b1ae7b78-182a-459e-ab28-f743e43f8293).  
  
## <a name="options"></a>Opciones  
**Índice espacial seleccionado**  
Enumera los índices espaciales existentes. Seleccione un índice para mostrar sus propiedades. Si la lista está vacía, no se han definido índices espaciales para la tabla.  
  
**Agregar**  
Crea un nuevo índice espacial.  
  
**Eliminar**  
Elimina el índice espacial seleccionado en la lista **Índice espacial seleccionado** .  
  
**Celdas por objeto**  
Indica el número de celdas por objeto de teselación que se pueden usar para un único objeto espacial en el índice. Este número puede ser un entero comprendido entre 1 y 8192, ambos incluidos. El valor predeterminado es 16.  
  
Si un objeto abarca más celdas de las especificadas mediante *n*, la indización usa tantas celdas como sean necesarias para proporcionar una teselación de nivel superior completa. En tales casos, un objeto podría recibir más celdas de las especificadas. En este caso, el número máximo es la cantidad de celdas generadas por la cuadrícula de nivel superior, que depende de la densidad de **Nivel 1** .  
  
**Columnas**  
Indica el nombre de la columna y el criterio de ordenación.  
  
**IsSpatialIndex**  
Indica que se ha seleccionado un índice espacial.  
  
**Nivel 1**  
Indica la densidad de la cuadrícula del primer nivel (superior).  
  
**Nivel 2**  
Indica la densidad de la cuadrícula del segundo nivel.  
  
**Nivel 3**  
Indica la densidad de la cuadrícula del tercer nivel.  
  
**Nivel 4**  
Indica la densidad de la cuadrícula del cuarto nivel.  
  
**Esquema de teselación**  
Indica el esquema de teselación:  
  
Opciones de la columna**Geometría** :  
  
-   **Cuadrícula de geometría** para una columna de geometría  
  
-   **Cuadrícula de geografía** para una columna de geografía  
  
**Tipo**  
Indica que se ha seleccionado un índice espacial.  
  
**X máxima**  
Especifica la coordenada X de la esquina superior derecha del cuadro de límite. Esta propiedad está atenuada si el **Esquema de teselación** es **Cuadrícula de geografía**.  
  
**X mínima**  
Especifica la coordenada X de la esquina inferior izquierda del cuadro de límite. Esta propiedad está atenuada si el **Esquema de teselación** es **Cuadrícula de geografía**.  
  
**Y máxima**  
Especifica la coordenada y de la esquina superior derecha del cuadro de límite. Esta propiedad está atenuada si el **Esquema de teselación** es **Cuadrícula de geografía**.  
  
**Y mínima**  
Especifica la coordenada Y de la esquina inferior izquierda del cuadro de límite. Esta propiedad está atenuada si el **Esquema de teselación** es **Cuadrícula de geografía**.  
  
**Identidad**  
Expandido, muestra los campos de propiedades **Nombre** y **Descripción** .  
  
**(Nombre)**  
Muestra el nombre del índice espacial. Cuando se crea un nuevo índice, aparece un nombre predeterminado que se genera a partir de la tabla de la ventana que está activa en el Diseñador de tablas. Este nombre se puede cambiar en cualquier momento.  
  
**Descripción**  
Describe el índice. Para escribir una descripción más detallada, haga clic en **Descripción** y, a continuación, en el botón de puntos suspensivos (**…**) situado a la derecha del campo de propiedad. De este modo, obtendrá un área más grande en la que escribir el texto.  
  
**Categoría Diseñador de tablas**  
Expandido, muestra información sobre las propiedades de este índice espacial.  
  
**Especificación de relleno**  
Expandido, muestra información sobre **Factor de relleno** y **Rellenar índice**.  
  
**Factor de relleno**  
Especifica qué porcentaje de la página de índice puede rellenar el sistema. Cuando una página está llena, si se agregan datos nuevos, el sistema debe dividirla, lo que perjudica al rendimiento.  
  
-   El valor 100 significa que las páginas estarán llenas y que utilizarán el menor volumen posible de espacio de almacenamiento, pero es la opción menos eficiente. Este valor debe utilizarse únicamente cuando no se van a efectuar cambios en los datos, como por ejemplo, en una tabla de solo lectura.  
  
-   Un valor más bajo deja más espacio vacío en las páginas de datos, lo que reduce la necesidad de dividir las páginas de datos cuando los índices aumentan, pero requiere más espacio de almacenamiento. Este valor es más adecuado cuando se vayan a producir cambios en los datos de la tabla.  
  
**Rellenar índice**  
Proporciona a las páginas de este índice el mismo porcentaje de espacio vacío (relleno) especificado en **Factor de relleno**.  
  
**Bloqueos de página permitidos**  
Especifica si se permite el bloqueo de páginas en este índice. Permitir o denegar el bloqueo de página afecta al rendimiento de la base de datos.  
  
**Volver a calcular** **estadísticas**  
Especifica si se deben calcular estadísticas nuevas cuando se crea el índice. Al volver a calcular las estadísticas, se ralentiza la generación de índices, pero suele mejorar el rendimiento de las consultas.  
  
**Bloqueos de fila permitidos**  
Especifica si se permite el bloqueo de filas en este índice. Permitir o denegar el bloqueo de fila afecta al rendimiento de la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Información general sobre los índices espaciales](http://msdn.microsoft.com/en-us/b1ae7b78-182a-459e-ab28-f743e43f8293)  
  

