---
title: "Gu&#237;a de arquitectura de p&#225;ginas y extensiones | Microsoft Docs"
ms.custom: ""
ms.date: "10/21/2016"
ms.prod: "sql-non-specified"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "guía de arquitectura de páginas y extensiones"
  - "guía, arquitectura de páginas y extensiones"
ms.assetid: 83a4aa90-1c10-4de6-956b-7c3cd464c2d2
caps.latest.revision: 2
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 2
---
# Gu&#237;a de arquitectura de p&#225;ginas y extensiones
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

La página es la unidad fundamental del almacenamiento de datos en SQL Server. Una extensión es una colección de ocho páginas físicamente contiguas. Las extensiones ayudan a administrar las páginas con eficacia. En esta guía se describen las estructuras de datos que se utilizan para administrar páginas y extensiones en todas las versiones de SQL Server. Comprender la arquitectura de las páginas y las extensiones es importante para diseñar y desarrollar bases de datos que funcionen eficazmente.

## Páginas y extensiones

La unidad fundamental del almacenamiento de datos en SQL Server es la página. El espacio en disco asignado a un archivo de datos (.mdf o .ndf) en una base de datos se divide lógicamente en páginas numeradas de forma contigua de 0 a n. Las operaciones de E/S de disco se realizan en el nivel de página. Es decir, SQL Server lee o escribe páginas de datos enteras.

Las extensiones son una colección de ocho páginas físicamente contiguas; se utilizan para administrar las páginas de forma eficaz. Todas las páginas se almacenen en extensiones.

### Páginas

En SQL Server, el tamaño de página es de 8 KB. Esto significa que las bases de datos de SQL Server tienen 128 páginas por megabyte. Cada página empieza con un encabezado de 96 bytes, que se utiliza para almacenar la información del sistema acerca de la página. Esta información incluye el número de página, el tipo de página, el espacio disponible en la página y el Id. de unidad de asignación del objeto propietario de la página.

En la siguiente tabla se muestran los tipos de página utilizados en los archivos de datos de una base de datos de SQL Server.

|Tipo de página | Contenido |
|-------|-------|
|Data |Filas de datos con todos los datos, excepto los datos de text, ntext, image, nvarchar(max), varchar(max), varbinary(max) y xml, cuando el texto de la fila está configurado en ON. |
|Índice |Entradas de índice. |
|Prueba/imagen |Tipos de datos de objetos grandes: (datos de text, ntext, image, nvarchar(max), varchar(max), varbinary(max) y xml) <br> Columnas de longitud variable cuando la fila de datos supera los 8 KB: (varchar, nvarchar, varbinary y sql_variant) |
|Mapa de asignación global, Mapa de asignación global compartido |Información acerca de si se han asignado las extensiones. |
|Espacio disponible en páginas (PFS) |Información acerca de la asignación de páginas y el espacio disponible disponible en las páginas. |
|Mapa de asignación de índices |Información acerca de las extensiones utilizadas por una tabla o un índice por unidad de asignación. |
|mapa cambiado masivamente |Información acerca de las extensiones modificadas por operaciones masivas desde la última instrucción BACKUP LOG por unidad de asignación. |
|Mapa cambiado diferencial |Información acerca de las extensiones que han cambiado desde la última instrucción BACKUP DATABASE por unidad de asignación. |

> [!NOTE]
> Los archivos de registro no contienen páginas, contienen series de registros.

Las filas de datos se colocan en las páginas una a continuación de otra, empezando inmediatamente después del encabezado. Al final de la página, comienza una tabla de desplazamiento de fila y cada una de esas tablas contiene una entrada para cada fila de la página. Cada entrada registra la distancia del primer byte de la fila desde el inicio de la página. Las entradas de la tabla de desplazamiento de fila están en orden inverso a la secuencia de las filas de la página.

![page_architecture](../relational-databases/media/page-architecture.gif)

**Compatibilidad con filas largas**  

Las filas no pueden abarcar páginas; no obstante, se pueden apartar de la página de la fila ciertas partes de la fila para que ésta pueda tener un tamaño mucho mayor. La cantidad máxima de datos y de sobrecarga que está contenida en una única fila de una página es de 8.060 bytes (8 KB). Sin embargo, esto no incluye los datos almacenados en el tipo de página Texto o imagen. Esta restricción es menos estricta para tablas que contienen columnas varchar, nvarchar, varbinary o sql_variant. Cuando el tamaño de fila total de todas las columnas variables y fijas de una tabla excede el límite de 8060 bytes, SQL Server mueve dinámicamente una o más columnas de longitud variable a páginas de la unidad de asignación ROW_OVERFLOW_DATA, empezando por la columna con el mayor ancho. Esto se realiza cuando una operación de inserción o actualización aumenta el tamaño total de la fila más allá del límite de 8060 bytes. Cuando una columna se mueve a una página de la unidad de asignación ROW_OVERFLOW_DATA, se mantiene un puntero de 24 bytes de la página original de la unidad de asignación IN_ROW_DATA. Si una operación posterior reduce el tamaño de la fila, SQL Server vuelve a mover las columnas dinámicamente a la página de datos original. 


### Extents 

Las extensiones son la unidad básica en la que se administra el espacio. Una extensión consta de ocho páginas contiguas físicamente, es decir 64 KB. Esto significa que las bases de datos de SQL Server tienen 16 extensiones por megabyte.

Para hacer que la asignación de espacio sea eficaz, SQL Server no asigna extensiones completas a tablas con pequeñas cantidades de datos. SQL Server tiene dos tipos de extensiones: 

* Las extensiones uniformes son propiedad de un único objeto; solo el objeto propietario puede utilizar las ocho páginas de la extensión.
* Las extensiones mixtas, que pueden estar compartidas por hasta ocho objetos. Cada una de las 8 páginas de la extensión puede ser propiedad de un objeto diferente.


A las tablas o índices nuevos se les suelen asignar páginas de extensiones mixtas. Cuando la tabla o el índice crecen hasta el punto de ocupar ocho páginas, se pasan a extensiones uniformes para las posteriores asignaciones. Si crea un índice de una tabla existente que dispone de filas suficientes para generar ocho páginas en el índice, todas las asignaciones del índice están en extensiones uniformes.

![extensiones](../relational-databases/media/extents.gif)

## Administrar las asignaciones de extensiones y el espacio disponible 

Las estructuras de datos de SQL Server que administran asignaciones de extensiones y realizan un seguimiento del espacio disponible tienen una estructura relativamente sencilla. Esto tiene las siguientes ventajas: 

* La información del espacio libre está densamente empaquetada, de modo que esta información está contenida en relativamente pocas páginas.   
  Esto aumenta la velocidad al reducir la cantidad de lecturas del disco necesarias para recuperar la información de asignación. También incrementa la posibilidad de que las páginas de asignación permanezcan en la memoria, lo que elimina aún más lecturas. 

* La mayor parte de la información de asignación no está encadenada. Esto simplifica el mantenimiento de la información de asignación.    
  La asignación o cancelación de asignación de las páginas se puede hacer con más rapidez. Esto reduce el conflicto entre las tareas simultáneas que necesiten asignar o cancelar la asignación de páginas. 

### Administrar las asignaciones de extensiones

SQL Server utiliza dos tipos de mapas de asignación para registrar la asignación de las extensiones: 

* Mapa de asignación global (GAM, Global Allocation Map)   
  Las páginas GAM registran las extensiones que han sido asignadas. Cada GAM cubre 64.000 extensiones o casi 4 GB de datos. La página GAM tiene un bit por cada extensión del intervalo que cubre. Si el bit es 1, la extensión está disponible; si el bit es 0, la extensión está asignada. 

* Mapa de asignación global compartido (SGAM, Shared Global Allocation Map)   
  Las páginas SGAM registran las extensiones que actualmente se están utilizando como extensiones mixtas y además tienen al menos una página sin utilizar. Cada SGAM cubre 64.000 extensiones o casi 4 GB de datos. La página SGAM tiene un bit por cada extensión del intervalo que cubre. Si el bit es 1, la extensión se está utilizando como extensión mixta y tiene una página disponible. Si el bit es 0, la extensión no se utiliza como extensión mixta o se trata de una extensión mixta cuyas páginas están todas en uso. 

Todas las extensiones tienen establecidos los siguientes patrones de bits en las página GAM y SGAM, basados en su uso actual. 

|Uso actual de la extensión | Bit en GAM | Bit en SGAM |
|---------|----------|------| 
|Disponible, no se utiliza |1 |0 |
|Extensión uniforme o extensión mixta completa |0 |0 |
|Extensión mixta con páginas disponibles |0 |1 |
 
Esto hace que los algoritmos de administración de las extensiones sean sencillos. Para asignar una extensión uniforme, el motor de base de datos busca un bit 1 en la página GAM y lo establece en 0. Para buscar una extensión mixta con páginas disponibles, el motor de base de datos busca un bit 1 en la página SGAM. Para asignar una extensión mixta, el motor de base de datos busca 1 bit en la página GAM, lo establece en 0 y, a continuación, establece también en 1 el bit correspondiente de la página SGAM. Para desasignar una extensión, el motor de base de datos se asegura de que el bit de la página GAM esté establecido en 1 y el bit de la página SGAM en 0. Los algoritmos internos usados realmente por el motor de base de datos son más complejos que los mencionados aquí, puesto que el motor de base de datos distribuye los datos en la base de datos de manera uniforme. Sin embargo, incluso los algoritmos reales quedan simplificados al no tener que administrar cadenas de información de asignación de extensiones.

### Realizar un seguimiento del espacio libre

Las páginas Espacio disponible en páginas (PFS, Page Free Space) registran el estado de asignación de cada página, si una página concreta está asignada y la cantidad de espacio libre en cada página. La PFS tiene un byte por página, que registra si la página está asignada y, en tal caso, si está vacía, llena entre el 1 y el 50%, entre el 51 y el 80%, entre el 81 y el 95% o entre el 96 y el 100%.

Una vez que se ha asignado una extensión a un objeto, el motor de base de datos utiliza las páginas PFS para registrar las páginas de la extensión que están asignadas o libres. Esta información se utiliza cuando el motor de base de datos tiene que asignar una nueva página. La cantidad de espacio libre de una página solo se mantiene en páginas de texto e imagen y de montón. Se utiliza cuando el motor de base de datos tiene que buscar una página con espacio libre disponible para almacenar una fila recién insertada. Los índices no necesitan que se haga un seguimiento del espacio libre en páginas, porque el punto en el que se inserta una nueva fila se establece mediante los valores de clave del índice.

La página PFS es la primera página que sigue a la página de encabezado de archivo en un archivo de datos (con el número de página 1). A continuación aparece una página GAM (con el número de página 2), seguida de una página SGAM (página 3). Hay una página PFS de aproximadamente 8.000 páginas de tamaño después de la primera página PFS. Hay otras 64.000 extensiones de la página GAM después de la primera página GAM en la página 2, y otras 64.000 extensiones de la página SGAM después de la primera página SGAM en la página 3. En la siguiente ilustración se muestra la secuencia de páginas que usa el motor de base de datos para asignar y administrar extensiones.

![manage_extents](../relational-databases/media/manage-extents.gif)

## Administrar el espacio utilizado por los objetos 

Una página del Mapa de asignación de índices (IAM) asigna las extensiones en una parte de 4 GB de un archivo de base de datos utilizado por una unidad de asignación. Existen tres tipos de unidades de asignación:

* IN_ROW_DATA   
    Contiene una partición de un montón o un índice.

* LOB_DATA   
   Contiene tipos de datos de objetos grandes (LOB), como xml, varbinary(max) y varchar(max).

* ROW_OVERFLOW_DATA   
   Contiene datos de longitud variable almacenados en columnas varchar, nvarchar, varbinary o sql_variant que superan el límite de tamaño de fila de 8060 bytes. 

Cada partición de un montón o un índice contiene al menos una unidad de asignación IN_ROW_DATA. También puede contener una unidad de asignación LOB_DATA o ROW_OVERFLOW_DATA en función del esquema del montón o el índice. Para obtener más información acerca de las unidades de asignación, vea Organización de tablas e índices.

Una página IAM cubre un intervalo de 4 GB en un archivo, lo que equivale a la cobertura de una página GAM o SGAM. Si la unidad de asignación contiene extensiones de más de un archivo o más de un intervalo de 4 GB de un archivo, se vincularán varias páginas IAM en una cadena IAM. Por lo tanto, cada unidad de asignación tiene como mínimo una página IAM para cada archivo en el que tiene extensiones. También puede haber más de una página IAM en un archivo si el intervalo de las extensiones del archivo asignado a la unidad de asignación supera el intervalo que una sola página IAM puede registrar. 

![iam_pages](../relational-databases/media/iam-pages.gif)

Las páginas IAM se asignan según se necesitan para cada unidad de asignación y se ubican en el archivo de forma aleatoria. La vista de sistema sys.system_internals_allocation_units señala la primera página IAM de la unidad de asignación. Todas las páginas IAM de esa unidad de asignación se vinculan en una cadena.

> [!IMPORTANT]
> La vista de sistema sys.system_internals_allocation_units se ha diseñado para uso interno y está sujeta a cambios, por lo que la compatibilidad no está garantizada.

![iam_chain](../relational-databases/media/iam-chain.gif)
 
Páginas IAM vinculadas en una cadena por unidad de asignación Una página IAM tiene un encabezado que indica la extensión inicial del intervalo de extensiones asignado por la página IAM. La página IAM también tiene un mapa de bits grande en el que cada bit representa una extensión. El primer bit del mapa representa la primera extensión del intervalo, el segundo bit representa la segunda extensión, etc. Si un bit es 0, la extensión que representa no está asignada a la unidad de asignación propietaria de IAM. Si el bit es 1, la extensión que representa está asignada a la unidad de asignación propietaria de la página IAM.

Si el motor de base de datos de SQL Server necesita insertar una fila nueva y no hay espacio disponible en la página actual, utiliza las páginas IAM y PFS para buscar una página para la asignación o, en el caso de un montón o una página de texto o imagen, una página con espacio suficiente para contener la fila. El motor de base de datos utiliza las páginas IAM para buscar las extensiones asignadas a la unidad de asignación. Para cada extensión, el motor de base de datos busca las páginas PFS para ver si existe una página que se pueda utilizar. Cada página IAM y PFS cubre muchas páginas de datos, por lo que en una base de datos hay pocas páginas IAM y PFS. Esto significa que las páginas IAM y PFS están generalmente en el grupo de búferes de SQL Server y se pueden buscar con rapidez. Para los índices, el punto de inserción de una nueva fila lo establece la clave de índice. En este caso, el proceso de búsqueda descrito anteriormente no se produce.

El motor de base de datos solo asigna una nueva extensión a una unidad de asignación cuando no puede encontrar rápidamente una página en una extensión existente con espacio suficiente para almacenar la fila que se va a insertar. El motor de base de datos asigna las extensiones entre las que están disponibles en el grupo de archivos siguiendo un algoritmo de asignación proporcional. Si un grupo de archivos tiene dos archivos, uno de los cuales tiene el doble de espacio disponible que el otro, asignará dos páginas del archivo con más espacio disponible por cada página asignada del otro archivo. Esto significa que los archivos de un grupo de archivos tienen un porcentaje de espacio utilizado similar. 

 
## Realizar un seguimiento de las extensiones modificadas 

SQL Server utiliza dos estructuras de datos internas para realizar un seguimiento de las extensiones modificadas mediante operaciones de copia masiva y de las extensiones modificadas desde la última copia de seguridad completa. Esas estructuras de datos aceleran en gran medida las copias de seguridad diferenciales. También aceleran el registro de las operaciones de copia masiva cuando una base de datos utiliza el modelo de recuperación optimizado para cargas masivas de registros. Al igual que las páginas del mapa de asignación global (GAM) y del mapa de asignación global compartido (SGAM), estas nuevas estructuras son mapas de bits en los que cada bit representa una única extensión. 

* Mapa cambiado diferencial (DCM)   
   Realiza un seguimiento de las extensiones que han cambiado desde la última instrucción BACKUP DATABASE. Si el bit de una extensión es 1, ésta se ha modificado desde la última instrucción BACKUP DATABASE. Si el bit es 0, la extensión no se ha modificado. Las copias de seguridad diferenciales solo leen las páginas DCM para determinar las extensiones que se han modificado. Esto reduce enormemente el número de páginas que debe recorrer una copia de seguridad diferencial. El tiempo de ejecución de una copia de seguridad diferencial es proporcional al número de extensiones modificadas desde la última instrucción BACKUP DATABASE y no al tamaño global de la base de datos. 

* Mapa cambiado masivamente (BCM)   
   Realiza un seguimiento de las extensiones que se han modificado mediante operaciones de registro masivo desde la última instrucción BACKUP LOG. Si el bit de una extensión es 1, ésta se ha modificado mediante una operación de registro masivo después de la última instrucción BACKUP LOG. Si el bit es 0, la extensión no se ha modificado mediante operaciones de registro masivo. Aunque las páginas BCM aparecen en todas las bases de datos, son relevantes únicamente cuando la base de datos está utilizando el modelo de recuperación optimizado para cargas masivas de registros. En este modelo de recuperación, cuando se ejecuta BACKUP LOG, el proceso de copia de seguridad recorre los BCM buscando extensiones que se hayan modificado. A continuación incluye dichas extensiones en la copia de seguridad del registro. Esto permite recuperar operaciones de registro masivo si se restaura la base de datos a partir de una copia de seguridad y una secuencia de copias de seguridad de registro de transacciones. Las páginas BCM no son relevantes en una base de datos que está utilizando el modelo de recuperación simple, porque no se registran las operaciones de registro masivo. No son relevantes en una base de datos que utiliza el modelo de recuperación completa, porque este modelo trata las operaciones de registro masivo como operaciones de registro completo. 

El intervalo entre las páginas DCM y BCM es el mismo que el intervalo entre las páginas GAM y SGAM, es decir, 64.000 extensiones. Las páginas DCM y BCM se colocan después de las páginas GAM y SGAM en un archivo físico:

![special_page_order](../relational-databases/media/special-page-order.gif)
 