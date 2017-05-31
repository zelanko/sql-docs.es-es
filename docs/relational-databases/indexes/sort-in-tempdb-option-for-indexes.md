---
title: "Opción SORT_IN_TEMPDB para índices | Microsoft Docs"
ms.custom: 
ms.date: 04/24/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SORT_IN_TEMPDB option
- disk space [SQL Server], indexes
- space [SQL Server], indexes
- tempdb database [SQL Server], indexes
- indexes [SQL Server], tempdb database
- index creation [SQL Server], tempdb database
ms.assetid: 754a003f-fe51-4d10-975a-f6b8c04ebd35
caps.latest.revision: 26
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1fa7ac1cb00252f855ba71b39fbccbe901365b00
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="sortintempdb-option-for-indexes"></a>Opción SORT_IN_TEMPDB para índices
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Cuando crea o vuelve a generar un índice, si establece la opción SORT_IN_TEMPDB en ON, puede indicar a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que use **tempdb** para almacenar los resultados de ordenación intermedios que se usan para generar el índice. Aunque esta opción aumenta la cantidad de espacio en disco temporal utilizado para crear un índice, reduce el tiempo que tarda en crear o volver a generar un índice cuando **tempdb** está en un conjunto de discos diferente al de la base de datos de usuario. Para obtener más información acerca de **tempdb**, vea [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md).  
  
## <a name="phases-of-index-building"></a>Fases de la generación de un índice  
 Para generar un índice, [!INCLUDE[ssDE](../../includes/ssde-md.md)] pasa por varias fases:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] recorre en primer lugar las páginas de datos de la tabla base para recuperar los valores clave y genera una fila hoja de índice para cada fila de datos. Cuando los búferes de orden interno se han llenado con las entradas del índice hoja, las entradas se ordenan y escriben en el disco como una ordenación intermedia. [!INCLUDE[ssDE](../../includes/ssde-md.md)] reanuda entonces el recorrido de páginas de datos hasta que los búferes de orden se llenan de nuevo. Este patrón de recorrido de varias páginas de datos seguido de la ordenación y escritura de una ejecución de orden continúa hasta que se han procesado todas las filas de la tabla base.  
  
     En un índice clúster, las filas hoja del índice son las filas de datos de la tabla, de manera que las ordenaciones intermedias contienen todas las filas de datos. En un índice no clúster, las filas hoja no contienen valores de columnas sin clave, pero suelen ser más pequeñas que un índice clúster. Si las claves de índice son grandes, o el índice incluye varias columnas sin clave, una ordenación no agrupada puede ser grande. Para obtener más información acerca de la inclusión de columnas sin clave, vea [Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md).  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] mezcla las ordenaciones de las filas hoja del índice en un único flujo ordenado. El componente de mezcla de ordenación de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se inicia con la primera página de cada ordenación, busca la clave más baja en todas las páginas y pasa esa fila hoja al componente de creación del índice. La siguiente clave más baja se procesa a continuación, después la siguiente, etc. Cuando se extrae la última fila del índice hoja de una página de ordenación, el proceso cambia a la página siguiente desde esa ordenación. Cuando se han procesado todas las páginas de una extensión de ordenación, la extensión se libera. Conforme se pasa cada fila de índice hoja al componente de creación del índice, se coloca en una página de índice hoja en el búfer. Cada página hoja se escribe conforme se llena. A medida que se escriben las páginas hoja, [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea también los niveles superiores del índice. Cada página de índice de nivel superior se escribe cuando se llena.  
  
## <a name="sortintempdb-option"></a>SORT_IN_TEMPDB, opción  
 Cuando SORT_IN_TEMPDB se establece en OFF (valor predeterminado), las ordenaciones se almacenan en el grupo de archivos de destino. Durante la primera fase de la creación del índice, las lecturas alternas de las páginas de la tabla base y las escrituras de las ordenaciones mueven los cabezales de lectura/escritura del disco de un área a otra del disco. Los cabezales están en el área de páginas de datos cuando se recorren las páginas de datos. Se mueven a un área de espacio disponible cuando los búferes de orden se llenan y se tiene que escribir la ordenación actual en el disco. A continuación, vuelven al área de páginas de datos cuando se reanuda el recorrido de páginas de la tabla. El movimiento de los cabezales de lectura/escritura es superior en la segunda fase. En ese momento, el proceso de ordenación está alternando lecturas de cada área de ordenación. Tanto las ordenaciones como las nuevas páginas de índice se crean en el grupo de archivos de destino, lo que significa que, al mismo tiempo que [!INCLUDE[ssDE](../../includes/ssde-md.md)] está repartiendo lecturas entre las ordenaciones, tiene que saltar periódicamente a las extensiones de índice para escribir nuevas páginas de índice conforme se llenan.  
  
 Si la opción SORT_IN_TEMPDB se ha establecido en ON y **tempdb** está en un conjunto de discos diferente del grupo de archivos de destino, durante la primera fase, las lecturas de las páginas de datos tienen lugar en un disco diferente que las escrituras en el área de trabajo de ordenación de **tempdb**. Esto significa que las lecturas del disco de las claves de datos tienden a proceder en serie en el disco, y las escrituras en el disco **tempdb** también tienden a ser en serie, igual que las escrituras para crear el índice final. Incluso si otros usuarios están utilizando la base de datos y están teniendo acceso a diferentes direcciones de disco, el patrón global de lecturas y escrituras es más eficaz cuando se especifica SORT_IN_TEMPDB que cuando no se especifica.  
  
 La opción SORT_IN_TEMPDB puede mejorar la contigüidad de extensiones de índice, especialmente si la operación CREATE INDEX no se procesa en paralelo. Las extensiones del área de trabajo de ordenación se liberan de una manera en cierto modo aleatoria con respecto a su ubicación en la base de datos. Si las áreas de trabajo de ordenación están contenidas en el grupo de archivos de destino, a medida que se liberan las extensiones de trabajo de ordenación, pueden ser adquiridas por las solicitudes de extensiones para albergar la estructura de índice conforme ésta se crea. Esto puede hacer que las ubicaciones de las extensiones del índice sean aleatorias hasta cierto punto. Si las extensiones de orden se mantienen por separado en **tempdb**, la secuencia en la que se liberan no afecta a la ubicación de las extensiones del índice. Asimismo, cuando las ordenaciones intermedias se almacenan en **tempdb** en lugar del grupo de archivos de destino, hay más espacio disponible en el grupo de archivos de destino, lo que aumenta las posibilidades de que las extensiones del índice sean contiguas.  
  
 La opción SORT_IN_TEMPDB afecta únicamente a la instrucción actual. Los metadatos no registran que el índice se ordenó o no se ordenó en **tempdb**. Por ejemplo, si crea un índice no clúster utilizando la opción SORT_IN_TEMPDB y, más adelante, crea un índice clúster sin especificar la opción, [!INCLUDE[ssDE](../../includes/ssde-md.md)] no utiliza la opción cuando crea de nuevo el índice no clúster.  
  
> [!NOTE]  
>  Si no se necesita una operación de ordenación o si la ordenación se puede realizar en memoria, la opción SORT_IN_TEMPDB se omite.  
  
## <a name="disk-space-requirements"></a>Requisitos de espacio en disco  
 Si establece la opción SORT_IN_TEMPDB en ON, debe tener suficiente espacio de disco disponible en **tempdb** para contener las ordenaciones intermedias, así como suficiente espacio de disco disponible en el grupo de archivos de destino para contener el nuevo índice. La instrucción CREATE INDEX produce errores si no hay suficiente espacio disponible y hay alguna razón por la que las bases de datos no pueden crecer automáticamente para adquirir más espacio (como falta de espacio en el disco o el crecimiento automático desactivado).  
  
 Si SORT_IN_TEMPDB se establece en OFF, el espacio de disco disponible en el grupo de archivos de destino debe ser aproximadamente el tamaño del índice final. Durante la primera fase, se crean las ordenaciones y éstas requieren aproximadamente la misma cantidad de espacio que el índice final. Durante la segunda fase, cada extensión de ordenación se libera después de haberla procesado. Esto significa que las extensiones de ordenación se liberan más o menos a la misma velocidad a la que se adquieren extensiones para albergar las páginas del índice final; por tanto, los requisitos de espacio globales no exceden en gran medida el tamaño del índice final. Un efecto secundario de esto es que, si la cantidad de espacio disponible es muy próxima al tamaño del índice final, [!INCLUDE[ssDE](../../includes/ssde-md.md)] tenderá a reutilizar las extensiones de ordenación con mucha rapidez cuando se liberen. Puesto que las extensiones de ordenación se liberan de una manera en cierto modo aleatoria, esto reduce la continuidad de las extensiones del índice en este escenario. Si SORT_IN_TEMPDB se establece en OFF, la continuidad de las extensiones del índice mejora si hay suficiente espacio disponible en el grupo de archivos de destino que se pueda asignar a las extensiones del índice desde un grupo contiguo en lugar de hacerlo desde extensiones de ordenación cuya asignación ha sido cancelada recientemente.  
  
 Cuando crea un índice no clúster, debe tener como espacio disponible:  
  
-   Si SORT_IN_TEMPDB se establece en ON, debe haber suficiente espacio disponible en **tempdb** para almacenar las ordenaciones y suficiente espacio disponible en el grupo de archivos de destino para almacenar la estructura del índice final. Las ordenaciones contienen las filas hoja del índice.  
  
-   Si SORT_IN_TEMPDB se establece en OFF, el espacio disponible del grupo de archivos de destino debe ser lo suficientemente extenso como para almacenar la estructura del índice final. La continuidad de las extensiones del índice se puede mejorar si hay más espacio disponible.  
  
 Cuando crea un índice clúster en una tabla que carece de índices no clúster, debe tener disponible como espacio disponible:  
  
-   Si SORT_IN_TEMPDB se establece en ON, debe haber suficiente espacio disponible en **tempdb** para almacenar las ordenaciones. incluidas las filas de datos de la tabla, y suficiente espacio disponible en el grupo de archivos de destino para almacenar la estructura del índice final, incluidas las filas de datos de la tabla y del árbol b del índice. Puede ser preciso ajustar la estimación para factores como tener un tamaño de clave grande o un factor de relleno con un valor bajo.  
  
-   Si SORT_IN_TEMPDB se establece en OFF, el espacio disponible del grupo de archivos de destino debe ser lo suficientemente extenso como para almacenar la tabla final. Esto incluye la estructura del índice. La continuidad de la tabla y las extensiones del índice se puede mejorar si hay más espacio disponible.  
  
 Cuando crea un índice clúster en una tabla que tiene índices no clúster, debe tener disponible como espacio disponible:  
  
-   Si SORT_IN_TEMPDB se establece en ON, debe haber suficiente espacio disponible en **tempdb** para almacenar el conjunto de ordenaciones para el índice más grande, normalmente el índice agrupado, y suficiente espacio disponible en el grupo de archivos de destino para almacenar las estructuras finales de todos los índices. Esto incluye el índice clúster que contiene las filas de datos de la tabla.  
  
-   Si SORT_IN_TEMPDB se establece en OFF, el espacio disponible del grupo de archivos de destino debe ser lo suficientemente extenso como para almacenar la tabla final. Esto incluye las estructuras de todos los índices. La continuidad de la tabla y las extensiones del índice se puede mejorar si hay más espacio disponible.  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
 [Reorganizar y volver a generar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [Configure the index create memory Server Configuration Option](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md)  
  
 [Requisitos de espacio en disco para operaciones DDL de índice](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)  
  
  

