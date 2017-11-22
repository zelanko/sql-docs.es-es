---
title: Comportamiento de bloqueo (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c55c636e-b767-4a0c-8184-be991a10801f
caps.latest.revision: "27"
ms.openlocfilehash: 6f4b213942db85b9e7171d11d6b88512d3ad7779
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="locking-behavior"></a>Comportamiento del bloqueo
PDW de SQL Server utiliza bloqueos para garantizar la integridad de las transacciones y para mantener la coherencia de las bases de datos cuando varios usuarios tienen acceso a datos al mismo tiempo.  
  
## <a name="Basics"></a>Conceptos básicos de bloqueos  
**Modos de**  
  
PDW de SQL Server admite cuatro modos de bloqueos:  
  
Exclusivo  
El bloqueo exclusivo impide que escribir o leer desde el objeto bloqueado hasta que la transacción que mantiene que el bloqueo exclusivo se completa. No hay otros bloqueos de cualquier modo se permiten mientras el bloqueo exclusivo está en vigor. Por ejemplo, DROP TABLE y CREATE DATABASE utilizan un bloqueo exclusivo.  
  
Compartidos  
El bloqueo compartido prohíbe la iniciación de un bloqueo exclusivo en el objeto afectado, pero permite que todos los demás modos de bloqueo. Por ejemplo, la instrucción SELECT inicia un bloqueo compartido y por lo tanto, permite que varias consultas tener acceso a los datos seleccionados al mismo tiempo, pero impide las actualizaciones a los registros que se está leyendo, hasta que se complete la instrucción SELECT.  
  
ExclusiveUpdate  
El bloqueo ExclusiveUpdate prohíbe la escritura en el objeto bloqueado, pero permitir la lectura mediante el bloqueo compartido. No hay otros bloqueos se permiten mientras el bloqueo ExclusiveUpdate está en vigor. Por ejemplo, base de datos de copia de seguridad y restaurar la base de datos utilizan un bloqueo exclusivo de actualización.  
  
SharedUpdate  
El bloqueo SharedUpdate prohíbe modos de bloqueo exclusivo y ExclusiveUpdate y permite a los modos de bloqueo compartido y SharedUpdate en el objeto. SharedUpdate modifica un objeto, pero no restringir el acceso de lectura a él durante la modificación. Por ejemplo, INSERT y UPDATE usar un bloqueo SharedUpdate.  
  
**Clases de recursos**  
  
Se mantienen los bloqueos en las siguientes clases de objetos: base de datos, esquema, objeto (tabla, vista o procedimiento), aplicaciones (se usa internamente), EXTERNALDATASOURCE, EXTERNALFILEFORMAT y SCHEMARESOLUTION (un nivel de base de datos de bloqueo realizado al crear, modificar, o quitar objetos de esquema o los usuarios de base de datos). Estas clases de objetos pueden aparecer en la columna object_type de [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Notas generales  
Los bloqueos pueden aplicarse a las bases de datos, tablas o vistas.  
  
SQL Server PDW no implementa los niveles de aislamiento configurable. Admite el nivel de aislamiento READ_UNCOMMITTED de acuerdo con el estándar ANSI. Sin embargo, desde la lectura de las operaciones se ejecutan bajo READ_UNCOMMITTED, muy pocas operaciones de bloqueo realmente se producen o dar lugar a la contención en el sistema.  
  
PDW de SQL Server se basa en el motor de SQL Server subyacente para implementar el control de simultaneidad y bloqueo. Si las operaciones dar lugar a un interbloqueo de SQL Server subyacente en el mismo nodo, SQL Server PDW aprovecha la capacidad de detección de interbloqueos de SQL Server y finaliza una de las instrucciones bloqueo.  
  
> [!NOTE]  
> SQL Server no permite las instrucciones que se esperan de bloqueos bloquear las solicitudes de bloqueo más reciente. PDW de SQL Server no ha implementado totalmente este proceso. En SQL Server PDW, las solicitudes continuadas de nuevos bloqueos compartidos a veces pueden bloquear una solicitud anterior (pero en espera) a un bloqueo exclusivo. Por ejemplo, un **actualización** instrucción (lo que requiere un bloqueo exclusivo) puede estar bloqueado por bloqueos compartidos que se conceden en serie de **seleccione** instrucciones. Para resolver un proceso bloqueado (identificado revisando el [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), dejará de enviar nuevas solicitudes hasta que se ha cumplido el bloqueo exclusivo.  
  
## <a name="lock-definition-table"></a>Tabla de definición de bloqueo  
SQL Server admite los siguientes tipos de bloqueos. No todos los tipos de bloqueo están disponibles en el nodo de control, pero pudieron producirse en los nodos de proceso.  
  
-   Sch-S (estabilidad del esquema). Garantiza que un elemento de un esquema, como una tabla o un índice, no se quite mientras una sesión mantenga un bloqueo de estabilidad del esquema sobre él.  
  
-   Sch-M (modificación del esquema). Debe mantenerlo cualquier sesión que desee cambiar el esquema del recurso especificado. Garantiza que ninguna otra sesión se refiera al objeto indicado.  
  
-   S (compartido). La sesión que lo mantiene recibe acceso compartido al recurso.  
  
-   U (actualizar). Indica que se ha obtenido un bloqueo de actualización sobre recursos que finalmente se pueden actualizar. Se utiliza para evitar una forma común de interbloqueo que tiene lugar cuando varias sesiones bloquean recursos para una posible actualización en el futuro.  
  
-   X (exclusivo). La sesión que lo mantiene recibe acceso exclusivo al recurso.  
  
-   IS (intención compartida). Indica la intención de establecer bloqueos S en algún recurso subordinado de la jerarquía de bloqueos.  
  
-   IU (actualizar intención). Indica la intención de establecer bloqueos U en algún recurso subordinado de la jerarquía de bloqueos.  
  
-   IX (intención exclusiva). Indica la intención de colocar bloqueos X en algunos recursos subordinados en la jerarquía de bloqueos.  
  
-   SIU (actualizar intención compartida). Indica el acceso compartido a un recurso con la intención de obtener bloqueos de actualización sobre recursos subordinados en la jerarquía de bloqueos.  
  
-   SEIS (intención compartida exclusiva). Indica acceso compartido a un recurso con la intención de obtener bloqueos exclusivos sobre recursos subordinados de la jerarquía de bloqueos.  
  
-   UIX (actualizar intención exclusiva). Indica un bloqueo de actualización en un recurso con la intención de adquirir bloqueos exclusivos sobre recursos subordinados en la jerarquía de bloqueos.  
  
-   UNIDAD DE NEGOCIO. Utilizado en las operaciones masivas.  
  
-   RangeS_S (bloqueo de intervalo de claves compartido y de recursos compartidos). Indica recorrido de intervalo serializable.  
  
-   RangeS_U (bloqueo de intervalo de claves compartido y de recursos de actualización). Indica recorrido de actualización serializable.  
  
-   RangeI_N (Insertar intervalo de claves y recurso Null bloqueo). Se utiliza para probar los intervalos antes de insertar una clave nueva en un índice.  
  
-   RangeI_S. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y S.  
  
-   RangeI_U. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y U.  
  
-   RangeI_X. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y X.  
  
-   RangeX_S. Bloqueo de conversión de rango de claves, creado por una superposición de bloqueos RangeI_N y RangeS_S bloqueos.  
  
-   RangeX_U. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y RangeS_U.  
  
-   RangeX_X (bloqueo de intervalo de claves exclusivo y recurso exclusivo). Es un bloqueo de conversión que se utiliza cuando se actualiza una clave de un intervalo.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
