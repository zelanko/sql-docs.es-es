---
title: "El grupo de archivos con optimización para memoria | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 07cda4d0c3e3bf0dd604de193ceef602a36c0ca9
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="the-memory-optimized-filegroup"></a>El grupo de archivos con optimización para memoria
  Para crear tablas con optimización para memoria, primero debe crear un grupo de archivos con optimización para memoria. El grupo de archivos con optimización para memoria contiene uno o varios contenedores. Cada contenedor contiene archivos de datos, archivos delta o ambos tipos de archivos.  
  
 Aunque las filas de datos de las tablas SCHEMA_ONLY no se conservan y los metadatos de las tablas con optimización para memoria y los procedimientos almacenados compilados de forma nativa se almacenan en los catálogos tradicionales, el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] todavía requiere un grupo de archivos con optimización para memoria para que las tablas SCHEMA_ONLY con optimización para memoria proporcionen una experiencia uniforme para las bases de datos con tablas con optimización para memoria.  
  
 El grupo de archivos con optimización para memoria se basa en el grupo de archivos de FILESTREAM, con las diferencias siguientes:  
  
-   Solo puede crear un grupo de archivos con optimización para memoria por cada base de datos. Debe marcarse explícitamente el grupo de archivos como que contiene memory_optimized_data. Puede crear el grupo de archivos al crear la base de datos o puede agregarlo posteriormente:  
  
    ```  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   Es necesario agregar uno o varios contenedores al grupo de archivos MEMORY_OPTIMIZED_DATA. Por ejemplo:  
  
    ```  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   No es necesario habilitar la secuencia de archivos ([Habilitar y configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)) para crear un grupo de archivos con optimización para memoria. La asignación a la secuencia de archivos la realiza el motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   Puede agregar nuevos contenedores a un grupo de archivos con optimización para memoria. Quizás necesite un nuevo contenedor para expandir el almacenamiento necesario para la tabla con optimización para memoria durable y también para distribuir la E/S entre varios contenedores.  
  
-   El movimiento de datos con un grupo de archivos con optimización para memoria se optimiza en una configuración de grupo de disponibilidad AlwaysOn. A diferencia de los archivos de FILESTREAM que se envían a las réplicas secundarias, los archivos de punto de comprobación (de datos y delta) del grupo de archivos con optimización para memoria no se envían a las réplicas secundarias. Los archivos de datos y delta se crean mediante el registro de transacciones la réplica secundaria.  
  
 A continuación se indican las limitaciones del grupo de archivos con optimización para memoria:  
  
-   Una vez que crea un grupo de archivos con optimización para memoria, solo puede quitarlo si quita la base de datos. En un entorno de producción, no es probable que necesite quitar el grupo de archivos con optimización para memoria.  
  
-   No puede quitar un contenedor que no esté vacío ni mover pares de archivos de datos y delta a otro contenedor en el grupo de archivos con optimización para memoria.  
  
-   No puede especificar MAXSIZE para el contenedor.  
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurar un grupo de archivos con optimización para memoria  
 Debe considerar la posibilidad de crear varios contenedores en el mismo grupo de archivos con optimización para memoria y distribuirlos en distintas unidades para lograr más ancho de banda para transmitir los datos en memoria.  
  
 Al configurar el almacenamiento, debe proporcionar una cantidad de espacio en disco disponible que sea cuatro veces el tamaño de tablas durables con optimización para memoria. También debe asegurarse de que el subsistema de E/S admite los IOPS necesarios para la carga de trabajo. Si los pares de archivos de datos y delta se rellenan en las IOPS especificadas, necesita 3 veces esas IOPS para dar cabida a las operaciones de almacenamiento y mezcla. Puede agregar capacidad de almacenamiento e IOPS si agrega uno o varios contenedores al grupo de archivos con optimización para memoria.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
