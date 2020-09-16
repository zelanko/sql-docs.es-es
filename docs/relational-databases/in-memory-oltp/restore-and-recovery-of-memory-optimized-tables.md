---
title: Restauración y recuperación de tablas optimizadas para memoria | Microsoft Docs
description: Obtenga información sobre cómo la restauración de una base de datos que usa tablas optimizadas para memoria en SQL Server difiere de la restauración de una base de datos que usa únicamente tablas basadas en disco.
ms.custom: ''
ms.date: 12/31/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 73edcacffe6267d6a2692018a106a4eb055817e6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551264"
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Restauración y recuperación de tablas optimizadas para memoria
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

El mecanismo básico para recuperar o restaurar una base de datos que use tablas optimizadas para memoria es el mismo que el de una base de datos que solo usa tablas basadas en disco. Pero, a diferencia de las tablas basadas en disco, las tablas optimizadas para memoria deben cargarse en memoria antes de que la base de datos esté disponible para el acceso de usuario. Con este requisito se agrega un nuevo paso en la recuperación de la base de datos.  
  
Si el servidor no tiene suficiente memoria disponible, se produce un error en la recuperación de la base de datos y la base de datos se marca como sospechosa. Para resolver este problema, vea [Resolver problemas de memoria insuficiente](resolve-out-of-memory-issues.md). 
  
## <a name="factors-that-affect-load-time"></a>Factores que afectan al tiempo de carga
Durante las operaciones de restauración o recuperación, el motor OLTP en memoria lee los archivos delta y de datos para cargarlos en la memoria física. El tiempo de carga está determinado por:  
  
-   Cantidad de datos que se van a cargar.  
  
-   Ancho de banda secuencial de E/S.  
  
-   Grado de paralelismo, determinado por el número de contenedores de archivos y de núcleos del procesador.  
  
-   La cantidad de entradas de registro en la parte activa del registro que tienen que rehacerse.  

## <a name="phases-of-recovery"></a>Fases de recuperación
Cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia, cada base de datos pasa por un proceso de recuperación que consta de tres fases:  
  
1.  **Análisis**. En esta fase, se realiza un paso en los registros de transacciones activos para detectar las transacciones confirmadas y no confirmadas. El motor de OLTP en memoria identifica el punto de comprobación que se va a cargar y carga previamente sus entradas de registro de la tabla del sistema. También procesa algunas entradas del registro de asignación de archivos.  
  
2.  **Rehacer**. Esta fase se ejecuta simultáneamente en tablas basadas en disco y en tablas optimizadas para memoria.  
  
    - Para las tablas basadas en disco, la base de datos se mueve al punto actual en el tiempo y adquiere los bloqueos obtenidos por las transacciones no confirmadas.  
  
    - En el caso de las tablas optimizadas para memoria, los datos de los pares de archivos delta y de datos se cargan en memoria. A continuación, los datos se actualizan con el registro de transacciones activas en función del punto de control duradero.  
  
    Cuando las operaciones anteriores en las tablas optimizadas para memoria y las basadas en disco se completan, la base de datos está disponible para su acceso.  
  
3.  **Deshacer**. En esta fase, las transacciones no confirmadas se revierten.  

## <a name="process-for-improving-load-time"></a>Proceso para reducir el tiempo de carga
Cargar en memoria las tablas optimizadas para memoria puede afectar el rendimiento del objetivo de tiempo de recuperación (RTO). Para mejorar el tiempo de carga de los datos optimizados para memoria de los archivos delta y de datos, el motor de OLTP en memoria carga los archivos delta y de datos en paralelo como se indica a continuación:  
  
-   **Crear un filtro de mapas de delta**. Los archivos delta almacenan las referencias a las filas eliminadas. Un subproceso por contenedor lee los archivos delta y crea un filtro de mapas de delta. Un grupo de archivos de datos optimizado para memoria puede tener uno o varios contenedores.  
  
-   **Transmitir los archivos de datos**. Una vez creado el filtro de mapas de delta, se leen los archivos de datos utilizando tantos subprocesos como CPU lógicas haya. Cada subproceso lee las filas de datos, comprueba el mapa de delta asociado e inserta una fila en la tabla solo si esa fila no se ha marcado como eliminada. Esta parte de la recuperación puede estar limitada por la CPU en algunos casos como se indica en este diagrama:  
  
    ![Streaming de datos a tablas optimizadas para memoria](../../relational-databases/in-memory-oltp/media/memory-optimized-tables.gif "Streaming de datos a tablas optimizadas para memoria")  
  
## <a name="specific-cases-of-slow-load-times"></a>Casos específicos de tiempos de carga lentos
Las tablas optimizadas para memoria se pueden cargar normalmente en memoria a la velocidad de E/S, pero cargar las filas de datos en memoria es, a veces, más lento. Los casos específicos son:  
  
-   Un número bajo de depósitos para el índice de hash puede llevar a una colisión excesiva, con lo que la inserción de filas de datos será más lenta. Esto produce normalmente un uso de CPU elevado en su totalidad, especialmente al final de la recuperación. Si ha configurado el índice de hash correctamente, no debería afectar el tiempo de recuperación.  
  
-   Las tablas grandes optimizadas para memoria con un índice no agrupado o más de uno pueden producir un uso de CPU elevado. A diferencia de un índice de hash cuyo número de cubos se establece en el momento de su creación, los índices no agrupados aumentan de forma dinámica.  
  
## <a name="see-also"></a>Consulte también  
 [Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
