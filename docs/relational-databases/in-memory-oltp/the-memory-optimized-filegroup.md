---
title: El grupo de archivos con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 265419b25df79ce491567cf563188ac70cdccc42
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024971"
---
# <a name="the-memory-optimized-filegroup"></a>El grupo de archivos con optimización para memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para crear tablas optimizadas para memoria, primero debe crear un grupo de archivos optimizados para memoria. El grupo de archivos optimizados para memoria contiene uno o varios contenedores. Cada contenedor contiene archivos de datos, archivos delta o ambos tipos de archivos.  
  
 Aunque las filas de datos de las tablas `SCHEMA_ONLY` no se conservan y los metadatos de las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa se almacenan en los catálogos tradicionales, el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] todavía requiere un grupo de archivos optimizados para memoria para que las tablas `SCHEMA_ONLY` optimizadas para memoria proporcionen una experiencia uniforme para las bases de datos con tablas optimizadas para memoria.  
  
 El grupo de archivos optimizados para memoria se basa en el grupo de archivos de FILESTREAM, con las diferencias siguientes:  
  
-   Solo puede crear un grupo de archivos optimizados para memoria por cada base de datos. Debe marcarse explícitamente el grupo de archivos como que contiene memory_optimized_data. Puede crear el grupo de archivos al crear la base de datos o puede agregarlo posteriormente:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   Debe agregar uno o varios contenedores al grupo de archivos `MEMORY_OPTIMIZED_DATA`. Por ejemplo:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   No es necesario habilitar la secuencia de archivos ([Habilitar y configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)) para crear un grupo de archivos optimizados para memoria. La asignación a la secuencia de archivos la realiza el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   Puede agregar nuevos contenedores a un grupo de archivos optimizados para memoria. Quizás necesite un nuevo contenedor para expandir el almacenamiento necesario para la tabla optimizada para memoria durable y también para distribuir la E/S entre varios contenedores.  
  
-   El movimiento de datos con un grupo de archivos optimizados para memoria se optimiza en una configuración de grupo de disponibilidad AlwaysOn. A diferencia de los archivos de FILESTREAM que se envían a las réplicas secundarias, los archivos de punto de comprobación (de datos y delta) del grupo de archivos optimizados para memoria no se envían a las réplicas secundarias. Los archivos de datos y delta se crean mediante el registro de transacciones la réplica secundaria.  
  
Las limitaciones siguientes se aplican al grupo de archivos optimizados para memoria:  
  
-   Una vez que use un grupo de archivos optimizados para memoria, solo puede quitarlo si quita la base de datos. En un entorno de producción, no es probable que necesite quitar el grupo de archivos optimizados para memoria.  
  
-   No puede quitar un contenedor que no esté vacío ni mover pares de archivos de datos y delta a otro contenedor en el grupo de archivos optimizados para memoria.    
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurar un grupo de archivos con optimización para memoria  
Considere la posibilidad de crear varios contenedores en el mismo grupo de archivos optimizados para memoria y distribuirlos en otras unidades para lograr más ancho de banda para transmitir los datos en memoria. 
 
En un escenario de varios contenedores y varias unidades, los archivos de datos y delta se asignan por turnos (round robin) en los contenedores. El primer archivo de datos se asigna al primer contenedor y el archivo delta se asigna desde el siguiente contenedor, y este modelo de asignación se repite. Este esquema de asignación distribuye uniformemente los archivos de datos y delta entre los contenedores si tiene un número impar de unidades, cada una de ellas asignada a un contenedor. Sin embargo, si tiene un número par de unidades, cada una de ellas asignada a un contenedor, puede provocar un almacenamiento desequilibrado donde los archivos de datos se asignan a las unidades impares y los archivos delta se asignan a las unidades pares. Para obtener un flujo equilibrado de E/S en la recuperación, considere la posibilidad de colocar los pares de archivos de datos y delta en los mismos ejes o almacenamiento.
  
Al configurar el almacenamiento, debe proporcionar una cantidad de espacio en disco disponible que sea cuatro veces el tamaño de tablas durables optimizadas para memoria. También debe asegurarse de que el subsistema de E/S admita los IOPS necesarios para la carga de trabajo. Si los pares de archivos de datos y delta se rellenan en las IOPS especificadas, necesita el triple de esas IOPS para dar cabida a las operaciones de almacenamiento y combinación. Puede agregar capacidad de almacenamiento e IOPS si agrega uno o varios contenedores al grupo de archivos optimizados para memoria.  
 
> [!CAUTION]
> Si se establece un valor `MAXSIZE` para el grupo de archivos optimizados para memoria y los archivos de punto de control superan el tamaño máximo del contenedor, la base de datos se convertirá en SUSPECT.   
> En este caso no intente establecer la base de datos OFFLINE y ONLINE, lo que haría que permaneciera en un estado RECOVERY_PENDING.
  
## <a name="see-also"></a>Consulte también  
[Crear y administrar el almacenamiento de objetos optimizados para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[Opciones File y Filegroup de ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 

