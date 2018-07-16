---
title: Configurar SQL Server para que Use Soft-NUMA (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- non-uniform memory access
ms.assetid: 1af22188-e08b-4c80-a27e-4ae6ed9ff969
caps.latest.revision: 38
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 434e569b17fa70b6f6b3f4763e54e08e271dc99b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279567"
---
# <a name="configure-sql-server-to-use-soft-numa-sql-server"></a>Configurar SQL Server para que use NUMA de software (SQL Server)
Los procesadores de hoy en día tienen varios núcleos por socket. Normalmente, cada socket se representa como un solo nodo NUMA. El motor de base de datos de SQL Server crea particiones de las diversas estructuras internas y de los subprocesos de servicio por nodo NUMA. Con procesadores que contiene 10 o más núcleos por socket, utilizando software NUMA (NUMA de software) para dividir los nodos NUMA de hardware generalmente aumenta la escalabilidad y rendimiento.   

> [!NOTE]
> soft-NUMA no admite procesadores de agregado en caliente.
  
## <a name="automatic-soft-numa"></a>soft-NUMA automático

A partir de SQL Server 2014 Service Pack 2, siempre que el servidor de motor de base de datos detecta más de 8 procesadores físicos en el inicio, nodos soft-NUMA se crean automáticamente si la marca de seguimiento 8079 está habilitada como un parámetro de inicio. Núcleos de procesador con Hyper-Threading no se recoge cuando contar los procesadores físicos. Cuando el número de procesadores físicos detectado es más de 8 por socket, el servicio de motor de base de datos creará nodos soft-NUMA que lo ideal es que contienen 8 núcleos, pero pueden bajar a 5 o subir a 9 procesadores lógicos por nodo. El tamaño del nodo de hardware puede estar limitado por una máscara de afinidad de CPU. El número de nodos NUMA nunca superará el número máximo de nodos NUMA admitido.

Sin la marca de seguimiento, soft-NUMA está deshabilitada de forma predeterminada. Puede habilitar soft-NUMA con marca de seguimiento 8079. Para que el cambio del valor de esta configuración surta efecto, hay que reiniciar el motor de base de datos.

La siguiente ilustración muestra el tipo de información sobre soft-NUMA que verá en el registro de errores de SQL Server cuando SQL Server detecta nodos NUMA de hardware con más de 8 procesadores lógicos y si la marca de seguimiento 8079 está habilitada.

![Soft-NUMA](./media/soft-numa-sql-server/soft-numa.PNG)

## <a name="manual-soft-numa"></a>soft-NUMA manual
  
Para configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que use NUMA de forma manual, debe editar el registro para agregar una máscara de afinidad de configuración de nodo. La máscara soft-NUMA se puede establecer como una entrada del Registro binaria, DWORD (hexadecimal o decimal) o QWORD (hexadecimal o decimal). Para configurar más de las primeras 32 CPU use valores del Registro QWORD o BINARY. (Los valores QWORD no se pueden usar antes de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]). Debe reiniciar [!INCLUDE[ssDE](../../includes/ssde-md.md)] para configurar soft-NUMA.  
  
> [!TIP]  
>  Las CPU se numeran a partir de 0.  
  
 [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
 Considere el ejemplo siguiente. Un equipo con ocho CPU no dispone de NUMA de hardware. Se configuran tres nodos de NUMA de software. La instancia A de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se configura para que use las CPU 0 a 3. Una segunda instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se instala y configura para que use las CPU 4 a 7. El ejemplo se puede representar visualmente como:  
  
 `CPUs          0  1  2  3  4  5  6  7`  
  
 `Soft-NUMA   <-N0--><-N1-><----N2---->`  
  
 `SQL Server  <instance A ><instance B>`  
  
 La instancia A, que experimenta actividades de E/S importantes, tiene ahora dos subprocesos de E/S y un subprocesos de escritura diferida, mientras que la instancia B, que realiza operaciones que requieren un uso intensivo del procesador, solo tiene un subproceso de E/S y un subproceso de escritura diferida. Se pueden asignar diferentes cantidades de memoria a las instancias, pero, a diferencia de lo que ocurre con el NUMA de hardware, ambas reciben memoria del mismo bloque de memoria del sistema operativo y no hay afinidad entre la memoria y el procesador.  
  
 El subproceso de escritura diferida está enlazado a la vista del sistema operativo SQL de los nodos físicos de memoria de NUMA. Por consiguiente, siempre que el hardware se presente como nodos físicos de NUMA, será igual al número de subprocesos de escritura diferida que se creen. Para obtener más información, vea el artículo acerca de [cómo funciona: NUMA de software, subproceso de finalización de E/S, trabajos de escritura diferida y nodos de memoria](http://blogs.msdn.com/b/psssql/archive/2010/04/02/how-it-works-soft-numa-i-o-completion-thread-lazy-writer-workers-and-memory-nodes.aspx).  
  
> [!NOTE]  
>  Las claves del Registro de **Soft-NUMA** no se copian al actualizar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="set-the-cpu-affinity-mask"></a>Establecer la máscara de afinidad de la CPU  
  
1.  Ejecute la siguiente instrucción en la instancia A para configurarla de modo que use las CPU 0, 1, 2 y 3, y establezca la máscara de afinidad de la CPU:  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=0 TO 3;  
    ```  
  
2.  Ejecute la siguiente instrucción en la instancia B para configurarla de modo que use las CPU 4, 5, 6 y 7, y establezca la máscara de afinidad de la CPU:  
  
    ```  
    ALTER SERVER CONFIGURATION   
    SET PROCESS AFFINITY CPU=4 TO 7;  
    ```  
  
### <a name="map-soft-numa-nodes-to-cpus"></a>Asignar nodos NUMA de software a las CPU  
  
-   Mediante el programa Editor del Registro (regedit.exe), agregue las dos claves del Registro siguientes para asignar el nodo 0 de soft-NUMA a las CPU 0 y 1, el nodo 1 de soft-NUMA a las CPU 2 y 3, y el nodo 2 de soft-NUMA a las CPU 4, 5, 6 y 7.  
  
     En el ejemplo siguiente, suponga que tiene un servidor DL580 G9 con 18 núcleos por socket (en 4 sockets) y que cada socket está en su propio grupo K. La configuración NUMA de software que cree será parecida a la siguiente. (6 núcleos por nodo, 3 nodos por grupo, 4 grupos).  
  
    |Ejemplo de un servidor [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] con varios grupos K|Tipo|Nombre del valor|Datos del valor|  
    |------------------------------------------------------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node3|DWORD|Grupo|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node4|DWORD|Grupo|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node5|DWORD|Grupo|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node6|DWORD|Grupo|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node7|DWORD|Grupo|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node8|DWORD|Grupo|2|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|CPUMask|0x3F|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node9|DWORD|Grupo|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|CPUMask|0x0fc0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node10|DWORD|Grupo|3|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|CPUMask|0x3f000|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node11|DWORD|Grupo|3|  
  
     Otros ejemplos:  
  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Tipo|Nombre del valor|Datos del valor|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\NodeConfiguration\Node2|DWORD|Grupo|0|  
  
    > [!TIP]  
    >  Para especificar las CPU 60 a 63, use un valor QWORD de F000000000000000 o un valor binario de 1111000000000000000000000000000000000000000000000000000000000000.  
  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Tipo|Nombre del valor|Datos del valor|  
    |---------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\NodeConfiguration\Node2|DWORD|Grupo|0|  
  
    |SQL Server 2008 R2|Tipo|Nombre del valor|Datos del valor|  
    |------------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|Grupo|0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|Grupo|0|  
  
    |SQL Server 2008|Tipo|Nombre del valor|Datos del valor|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
    |SQL Server 2005|Tipo|Nombre del valor|Datos del valor|  
    |---------------------|----------|----------------|----------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node0|DWORD|CPUMask|0x03|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node1|DWORD|CPUMask|0x0c|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\90\NodeConfiguration\Node2|DWORD|CPUMask|0xf0|  
  
## <a name="see-also"></a>Vea también  
 [Asignación de puertos TCP/IP a nodos NUMA &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)   
 [affinity mask (opción de configuración del servidor)](affinity-mask-server-configuration-option.md)   
 [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql)  
  
  
