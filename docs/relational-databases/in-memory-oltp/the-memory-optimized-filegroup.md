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
manager: craigg
ms.openlocfilehash: 31c66aaacdcebfeabf43cc6466659e25d47d4d05
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606943"
---
# <a name="the-memory-optimized-filegroup"></a>El grupo de archivos con optimización para memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para crear tablas optimizadas para memoria, primero debe crear un grupo de archivos optimizados para memoria. El grupo de archivos optimizados para memoria contiene uno o varios contenedores. Cada contenedor contiene archivos de datos, archivos delta o ambos tipos de archivos.  
  
 Aunque las filas de datos de las tablas SCHEMA_ONLY no se conservan y los metadatos de las tablas optimizadas para memoria y los procedimientos almacenados compilados de forma nativa se almacenan en los catálogos tradicionales, el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] todavía requiere un grupo de archivos optimizados para memoria para que las tablas SCHEMA_ONLY optimizadas para memoria proporcionen una experiencia uniforme para las bases de datos con tablas optimizadas para memoria.  
  
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
  
-   Una vez que crea un grupo de archivos optimizados para memoria, solo puede quitarlo si quita la base de datos. En un entorno de producción, no es probable que necesite quitar el grupo de archivos optimizados para memoria.  
  
-   No puede quitar un contenedor que no esté vacío ni mover pares de archivos de datos y delta a otro contenedor en el grupo de archivos optimizados para memoria.  
  
-   No puede especificar `MAXSIZE` para el contenedor.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurar un grupo de archivos con optimización para memoria  
 Debe considerar la posibilidad de crear varios contenedores en el mismo grupo de archivos optimizados para memoria y distribuirlos en distintas unidades para lograr más ancho de banda para transmitir los datos en memoria.  
  
 Al configurar el almacenamiento, debe proporcionar una cantidad de espacio en disco disponible que sea cuatro veces el tamaño de tablas durables optimizadas para memoria. También debe asegurarse de que el subsistema de E/S admita los IOPS necesarios para la carga de trabajo. Si los pares de archivos de datos y delta se rellenan en las IOPS especificadas, necesita 3 veces esas IOPS para dar cabida a las operaciones de almacenamiento y mezcla. Puede agregar capacidad de almacenamiento e IOPS si agrega uno o varios contenedores al grupo de archivos optimizados para memoria.  
  
## <a name="see-also"></a>Ver también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
 [Archivos y grupos de archivos de base de datos](../../relational-databases/databases/database-files-and-filegroups.md) 
  
