---
title: Restaurar y recuperar tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
caps.latest.revision: 9
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e93ade38a2c90edba1551f1128571f0a7d5533aa
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37260811"
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Restaurar y recuperar tablas con optimización para memoria
  El mecanismo básico para recuperar o restaurar una base de datos con tablas optimizadas para memoria es similar al de las bases de datos con solo tablas basadas en disco. Pero a diferencia de las tablas basadas en disco, las tablas optimizadas para memoria deben cargarse en memoria antes de que la base de datos esté disponible para el acceso de usuario. Esto agrega un nuevo paso en la recuperación de la base de datos. Los pasos modificados en la recuperación de base de datos cambian de este modo:  
  
 Cuando se reinicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , cada base de datos pasa por una fase de recuperación que consta de las tres fases siguientes:  
  
1.  La fase de análisis. Durante esta fase, se realiza un paso en los registros de transacciones activos para detectar las transacciones confirmadas y no confirmadas. El motor de OLTP en memoria identifica el punto de comprobación que se va a cargar y carga previamente sus entradas de registro de la tabla del sistema. También procesará algunas entradas del registro de asignación de archivos.  
  
2.  La fase de rehacer. Esta fase se ejecuta simultáneamente en tablas basadas en disco y en tablas optimizadas para memoria.  
  
     Para las tablas basadas en disco, la base de datos se mueve al punto actual en el tiempo y adquiere los bloqueos obtenidos por las transacciones no confirmadas.  
  
     Para las tablas optimizadas para memoria, los datos de los pares de archivos delta y de datos se cargan en memoria y luego se actualizan los datos con el registro de transacciones activo en función del último punto de comprobación durable.  
  
     Cuando las operaciones anteriores en las tablas optimizadas para memoria y las basadas en disco se completan, la base de datos está disponible para su acceso.  
  
3.  La fase de deshacer. En esta fase, las transacciones no confirmadas se revierten.  
  
 Cargar en memoria las tablas optimizadas para memoria puede afectar el rendimiento del objetivo de tiempo de recuperación (RTO). Para mejorar el tiempo de carga de los datos optimizados para memoria de los archivos delta y de datos, el motor de OLTP en memoria carga los archivos delta y de datos en paralelo como se indica a continuación:  
  
-   Crear un filtro de mapas de delta. Los archivos delta almacenan las referencias a las filas eliminadas. Un subproceso por contenedor lee los archivos delta y crea un filtro de mapas de delta. (Un grupo de archivos de datos con optimización para memoria puede tener uno o varios contenedores).  
  
-   Transmitir los archivos de datos.  Una vez creado el filtro de mapas de delta, se leen los archivos de datos utilizando tantos subprocesos como CPU lógicas haya. Cada subproceso que lee el archivo de datos lee las filas de datos, comprueba el mapa de delta asociado e inserta únicamente la fila en la tabla si esta fila no se ha marcado como eliminada. Esta parte de la recuperación puede estar limitada por la CPU en algunos casos como se indica a continuación.  
  
 ![Tablas con optimización para memoria.](../../database-engine/media/memory-optimized-tables.gif "Tablas con optimización para memoria.")  
  
 Las tablas con optimización para memoria se pueden cargar normalmente en memoria a la velocidad de E/S pero hay casos que al cargar las filas de datos en memoria será más lento. Los casos específicos son:  
  
-   Un número bajo de cubos para el índice de hash puede llevar a una colisión excesiva con lo que la inserción de filas de datos será más lenta. Esto produce normalmente un uso de CPU muy elevado en su totalidad, sobre todo al final de la recuperación. Si ha configurado el índice de hash correctamente, no debería afectar el tiempo de recuperación.  
  
-   En tablas de gran tamaño optimizadas para memoria y con uno o varios índices no clúster (a diferencia de un índice de hash, cuyo número de cubos se establece en el momento de la creación), los índices no clúster aumentan dinámicamente, lo que da lugar a un uso elevado de la CPU.  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>Restaurar una base de datos con tablas con optimización para memoria  
 Sabe que tiene memoria suficiente en el servidor para restaurar una base de datos, pero hay un requisito de que la memoria necesaria para la base de datos se tenga en cuenta como parte de un grupo de recursos existente.  Sabe que no se puede crear el enlace al grupo de recursos antes de que exista la base de datos, por lo que realiza la restauración WITH NORECOVERY.  Esto hace que la imagen de disco de la base de datos se restaure y se cree la base de datos, pero no se consume memoria de OLTP en memoria debido a que la base de datos no se pone en línea.  
  
 En este punto, puede crear el grupo de recursos para el enlace de la base de datos y luego usar RESTORE WITH RECOVERY para poner en línea la base de datos restaurada.  Dado que el enlace se coloca antes de poner en línea la base de datos, su consumo de memoria de OLTP en memoria se tiene en cuenta correctamente. Esto requiere restaurar la base de datos solo una vez. El primer comando RESTORE es un comando informativo que solo lee el encabezado de copia de seguridad y el último comando solo desencadena una recuperación sin restaurar realmente ningún bit.  
  
## <a name="see-also"></a>Vea también  
 [Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](memory-optimized-tables.md)  
  
  
