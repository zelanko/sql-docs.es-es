---
title: Comportamiento de bloqueo - almacenamiento de datos paralelos | Microsoft Docs
description: Obtenga información sobre cómo Parallel Data Warehouse utiliza el bloqueo para garantizar la integridad de las transacciones y mantener la coherencia de las bases de datos cuando varios usuarios accedan a datos al mismo tiempo.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3f9862fed432036dcb4a3905fb3af1d3132349a5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280889"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>Comportamiento de bloqueo en el almacenamiento de datos paralelos
Obtenga información sobre cómo Parallel Data Warehouse utiliza el bloqueo para garantizar la integridad de las transacciones y mantener la coherencia de las bases de datos cuando varios usuarios accedan a datos al mismo tiempo.  
  
## <a name="Basics"></a>Conceptos básicos de bloqueos  
**Modos de**  
  
PDW de SQL Server admite cuatro modos de bloqueos:  
  
Exclusivo  
El bloqueo exclusivo impide escribir o leer desde el objeto bloqueado hasta que la transacción mantiene que un bloqueo exclusivo se completa. No se permiten ningún otros bloqueos de cualquier modo mientras el bloqueo exclusivo está vigente. Por ejemplo, DROP TABLE y CREATE DATABASE debe usar un bloqueo exclusivo.  
  
Compartidos  
El bloqueo compartido prohíbe la iniciación de un bloqueo exclusivo en el objeto afectado, pero permite que todos los demás modos de bloqueo. Por ejemplo, la instrucción SELECT inicia un bloqueo compartido y por lo tanto, permite que varias consultas tener acceso a los datos seleccionados al mismo tiempo, pero impide las actualizaciones a los registros que se está leyendo, hasta que se complete la instrucción SELECT.  
  
ExclusiveUpdate  
El bloqueo ExclusiveUpdate prohíbe la escritura en el objeto bloqueado, pero permitir la lectura mediante el bloqueo compartido. No se permiten ningún otros bloqueos mientras el bloqueo ExclusiveUpdate está vigente. Por ejemplo, base de datos de copia de seguridad y restaurar la base de datos utilizan un bloqueo de actualización exclusiva.  
  
SharedUpdate  
El bloqueo SharedUpdate prohíbe modos de bloqueo exclusivo y ExclusiveUpdate y permite que los modos de bloqueo compartido y SharedUpdate en el objeto. SharedUpdate modifica un objeto, pero no restringe el acceso de lectura a ella durante la modificación. Por ejemplo, INSERT y UPDATE utiliza un bloqueo SharedUpdate.  
  
**Clases de recursos**  
  
Se mantienen bloqueos en las siguientes clases de objetos: Base de datos, esquema, objeto (tabla, vista o procedimiento), aplicación (se usa internamente), EXTERNALDATASOURCE, EXTERNALFILEFORMAT y SCHEMARESOLUTION (un base de datos nivel bloqueo realizado al crear, modificar o quitar objetos de esquema o los usuarios de base de datos). Estas clases de objetos pueden aparecer en la columna object_type de [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Notas generales  
Los bloqueos pueden aplicarse a las bases de datos, tablas o vistas.  
  
PDW de SQL Server no implementa los niveles de aislamiento configurable. Admite el nivel de aislamiento READ_UNCOMMITTED según se define en el estándar ANSI. Sin embargo, desde la lectura de las operaciones se ejecutan bajo READ_UNCOMMITTED, muy pocas operaciones de bloqueo realmente se producen o causar contención en el sistema.  
  
PDW de SQL Server se basa en el motor de SQL Server subyacente para implementar el control de simultaneidad y el bloqueo. Si las operaciones de provocar un interbloqueo de SQL Server subyacente en el mismo nodo, PDW de SQL Server aprovecha la capacidad de detección de interbloqueo de SQL Server y finaliza una de las instrucciones bloqueos.  
  
> [!NOTE]  
> SQL Server no admite las instrucciones que están esperando bloqueos que se bloquee las solicitudes de bloqueo más reciente. PDW de SQL Server no ha implementado completamente este proceso. En SQL Server PDW, las solicitudes de nuevos bloqueos compartidos a veces pueden bloquear una solicitud anterior (pero en espera) para un bloqueo exclusivo. Por ejemplo, un **actualización** instrucción (lo que requiere un bloqueo exclusivo) puede estar bloqueada por bloqueos compartidos que se conceden para la serie de **seleccione** instrucciones. Para resolver un proceso bloqueado (identificado por revisar el [sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), dejará de enviar nuevas solicitudes hasta que se ha cumplido el bloqueo exclusivo.  
  
## <a name="lock-definition-table"></a>Tabla de definición de bloqueo  
SQL Server admite los siguientes tipos de bloqueos. No todos los tipos de bloqueo están disponibles en el nodo de control, pero pueden producirse en los nodos de proceso.  
  
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
  
-   BU. Utilizado en las operaciones masivas.  
  
-   RangeS_S (bloqueo de intervalo de claves compartido y recurso compartido). Indica recorrido de intervalo serializable.  
  
-   RangeS_U (intervalo de claves compartido y actualización de bloqueo de recurso). Indica recorrido de actualización serializable.  
  
-   RangeI_N (Insertar intervalo de claves y Null bloqueo de recurso). Se utiliza para probar los intervalos antes de insertar una clave nueva en un índice.  
  
-   RangeI_S. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y S.  
  
-   RangeI_U. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y U.  
  
-   RangeI_X. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y X.  
  
-   RangeX_S. Bloqueo de conversión de rango de claves, creado por una superposición de bloqueos RangeI_N y RangeS_S bloqueos.  
  
-   RangeX_U. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y RangeS_U.  
  
-   RangeX_X (intervalo de claves exclusivo y recursos exclusivos bloqueo). Es un bloqueo de conversión que se utiliza cuando se actualiza una clave de un intervalo.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[sys.dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
