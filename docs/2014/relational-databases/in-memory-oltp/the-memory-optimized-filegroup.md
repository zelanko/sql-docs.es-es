---
title: El grupo de archivos con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 64402f73fdf43c0ebcbeff338ed72d56d55227be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63155578"
---
# <a name="the-memory-optimized-filegroup"></a>El grupo de archivos con optimización para memoria
  Para crear tablas optimizadas para memoria, primero debe crear un grupo de archivos optimizados para memoria. El grupo de archivos optimizados para memoria contiene uno o varios contenedores. Cada contenedor contiene archivos de datos, archivos delta o ambos tipos de archivos.  
  
 Aunque las filas de datos de las tablas `SCHEMA_ONLY` no se conservan y los metadatos de las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa se almacenan en los catálogos tradicionales, el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] todavía requiere un grupo de archivos optimizados para memoria para que las tablas `SCHEMA_ONLY` optimizadas para memoria proporcionen una experiencia uniforme para las bases de datos con tablas optimizadas para memoria.  
  
 El grupo de archivos optimizados para memoria se basa en el grupo de archivos de FILESTREAM, con las diferencias siguientes:  
  
-   Solo puede crear un grupo de archivos optimizados para memoria por cada base de datos. Debe marcarse explícitamente el grupo de archivos como que contiene memory_optimized_data. Puede crear el grupo de archivos al crear la base de datos o puede agregarlo posteriormente:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   Es necesario agregar uno o varios contenedores al grupo de archivos MEMORY_OPTIMIZED_DATA. Por ejemplo:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   No es necesario habilitar la secuencia de archivos ([Habilitar y configurar FILESTREAM](../blob/enable-and-configure-filestream.md)) para crear un grupo de archivos optimizados para memoria. La asignación a la secuencia de archivos la realiza el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   Puede agregar nuevos contenedores a un grupo de archivos optimizados para memoria. Puede que necesite un nuevo contenedor para expandir el almacenamiento necesario para la tabla optimizada para memoria durable y también para distribuir la E/S entre varios contenedores.  
  
-   El movimiento de datos con un grupo de archivos optimizados para memoria se optimiza en una configuración de grupo de disponibilidad AlwaysOn. A diferencia de los archivos de FILESTREAM que se envían a las réplicas secundarias, los archivos de punto de comprobación (de datos y delta) del grupo de archivos optimizados para memoria no se envían a las réplicas secundarias. Los archivos de datos y delta se crean mediante el registro de transacciones la réplica secundaria.  
  
A continuación se indican las limitaciones del grupo de archivos optimizados para memoria:  
  
-   Una vez que crea un grupo de archivos optimizados para memoria, solo puede quitarlo si quita la base de datos. En un entorno de producción, no es probable que necesite quitar el grupo de archivos optimizados para memoria.  
  
-   No puede quitar un contenedor que no esté vacío ni mover pares de archivos de datos y delta a otro contenedor en el grupo de archivos optimizados para memoria.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurar un grupo de archivos con optimización para memoria  
Considere la posibilidad de crear varios contenedores en el mismo grupo de archivos optimizados para memoria y distribuirlos en otras unidades para lograr más ancho de banda para transmitir los datos en memoria.  
  
Al configurar el almacenamiento, debe proporcionar una cantidad de espacio en disco disponible que sea cuatro veces el tamaño de tablas durables optimizadas para memoria. Asegúrese de que el subsistema de E/S admite los IOPS necesarios para la carga de trabajo. Si los pares de archivos de datos y delta se rellenan en las IOPS especificadas, necesita el triple de esas IOPS para dar cabida a las operaciones de almacenamiento y combinación. Puede agregar capacidad de almacenamiento e IOPS si agrega uno o varios contenedores al grupo de archivos optimizados para memoria.  
  
En un escenario de varios contenedores y varias unidades, los archivos de datos y delta se asignan por turnos (round robin) en los contenedores. El primer archivo de datos se asigna al primer contenedor y el archivo delta se asigna desde el siguiente contenedor, y este modelo de asignación se repite. Este esquema de asignación distribuye uniformemente los archivos de datos y delta entre los contenedores si tiene un número impar de unidades, cada una de ellas asignada a un contenedor. Sin embargo, si tiene un número par de unidades, cada una de ellas asignada a un contenedor, puede provocar un almacenamiento desequilibrado donde los archivos de datos se asignan a las unidades impares y los archivos delta se asignan a las unidades pares. Para obtener un flujo equilibrado de E/S en la recuperación, considere la posibilidad de colocar los pares de archivos delta y de datos en lo mismos ejes o almacenamiento como se describe en el ejemplo siguiente.  

> [!CAUTION]
> Si se establece un valor `MAXSIZE` para el grupo de archivos optimizados para memoria y los archivos de punto de control superan el tamaño máximo del contenedor, la base de datos se convertirá en SUSPECT.   
> En este caso no intente establecer la base de datos OFFLINE y ONLINE, lo que haría que permaneciera en un estado RECOVERY_PENDING.
  
### <a name="example"></a>Ejemplo 
Considere la posibilidad de un grupo de archivos optimizados para memoria con dos contenedores: contenedor 1 unidad X y el contenedor 2 en la unidad Y.  
Puesto que la asignación de archivos de datos y delta se hace de modo round robin, el contenedor 1 solamente tendrá archivos de datos y el contenedor 2 solamente tendrá archivos delta, lo que produce un desequilibrio en las operaciones de almacenamiento y entrada/salida por segundo; además, los archivos de datos son mucho mayores que los archivos delta.    
Para distribuir archivos de datos y delta uniformemente en las unidades X e Y, cree cuatro contenedores en lugar de dos y asigne los dos primeros contenedores unidad X y los dos contenedores siguientes a la unidad Y.  
Con la asignación de round robin, el primero los datos y el primer archivo delta se asignarán desde container-1 y el contenedor 2 respectivamente, que se asignan a la unidad X.   
De forma similar, el siguiente archivo de datos y delta se asignarán desde contenedor 3 y 4, contenedor que se asignan a la unidad Y. Esto permite distribuir uniformemente los archivos delta y de datos a través de dos unidades.  
 
  
## <a name="see-also"></a>Vea también  
[Creación y administración del almacenamiento de objetos con optimización para memoria](creating-and-managing-storage-for-memory-optimized-objects.md)     
[Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md)    
  
