---
title: Comportamiento de bloqueo
description: Obtenga información sobre cómo el almacenamiento de datos paralelo utiliza el bloqueo para garantizar la integridad de las transacciones y mantener la coherencia de las bases de datos cuando varios usuarios tienen acceso a los datos al mismo tiempo.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: f3ecf5cf783b707b75c90dfa70d502e3c81d28c3
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401001"
---
# <a name="locking-behavior-in-parallel-data-warehouse"></a>Comportamiento de bloqueo en almacenamiento de datos paralelos
Obtenga información sobre cómo el almacenamiento de datos paralelo utiliza el bloqueo para garantizar la integridad de las transacciones y mantener la coherencia de las bases de datos cuando varios usuarios tienen acceso a los datos al mismo tiempo.  
  
## <a name="Basics"></a>Conceptos básicos de bloqueo  
**Formas**  
  
PDW de SQL Server admite cuatro modos de bloqueo:  
  
Exclusivo  
El bloqueo exclusivo prohíbe escribir o leer el objeto bloqueado hasta que se complete la transacción que contiene el bloqueo exclusivo. No se permiten otros bloqueos de ningún modo mientras el bloqueo exclusivo está en vigor. Por ejemplo, DROP TABLE y CREATE DATABASE usan un bloqueo exclusivo.  
  
Compartido  
El bloqueo compartido prohíbe la iniciación de un bloqueo exclusivo en el objeto afectado, pero permite todos los demás modos de bloqueo. Por ejemplo, la instrucción SELECT inicia un bloqueo compartido y, por lo tanto, permite que varias consultas tengan acceso a los datos seleccionados simultáneamente, pero impide que se lean las actualizaciones de los registros hasta que se complete la instrucción SELECT.  
  
ExclusiveUpdate  
El bloqueo ExclusiveUpdate prohíbe escribir en el objeto bloqueado, pero permite la lectura a través del bloqueo compartido. No se permiten otros bloqueos mientras el bloqueo ExclusiveUpdate está en vigor. Por ejemplo, BACKUP DATABASE y RESTOre DATABASE usan un bloqueo de actualización exclusivo.  
  
SharedUpdate  
El bloqueo SharedUpdate prohíbe los modos de bloqueo exclusivo y ExclusiveUpdate y permite los modos de bloqueo compartido y SharedUpdate en el objeto. SharedUpdate modifica un objeto, pero no restringe el acceso de lectura a él durante la modificación. Por ejemplo, INSERT y UPDATE usan un bloqueo SharedUpdate.  
  
**Clases de recursos**  
  
Los bloqueos se mantienen en las siguientes clases de objetos: base de datos, esquema, objeto (una tabla, vista o procedimiento), aplicación (usada internamente), EXTERNALDATASOURCE, EXTERNALFILEFORMAT y SCHEMARESOLUTION (se realiza un bloqueo de nivel de base de datos al crear, modificar o quitar objetos de esquema o usuarios de base de datos). Estas clases de objetos pueden aparecer en la object_type columna de [Sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md).  
  
## <a name="Remarks"></a>Notas generales  
Los bloqueos se pueden aplicar a bases de datos, tablas o vistas.  
  
PDW de SQL Server no implementa ningún nivel de aislamiento configurable. Admite el nivel de aislamiento READ_UNCOMMITTED tal y como se define en el estándar ANSI. Sin embargo, dado que las operaciones de lectura se ejecutan en READ_UNCOMMITTED, muy pocas operaciones de bloqueo se producen realmente o conducen a la contención en el sistema.  
  
PDW de SQL Server se basa en el motor de SQL Server subyacente para implementar el control de bloqueos y simultaneidad. Si las operaciones conducen a un interbloqueo de SQL Server subyacente dentro del mismo nodo, PDW de SQL Server aprovecha la capacidad de detección de interbloqueos de SQL Server y finaliza una de las instrucciones de bloqueo.  
  
> [!NOTE]  
> SQL Server no permite que las instrucciones que están esperando que los bloqueos se bloqueen mediante solicitudes de bloqueo más recientes. PDW de SQL Server no ha implementado completamente este proceso. En PDW de SQL Server, las solicitudes continuas para nuevos bloqueos compartidos a veces pueden bloquear una solicitud anterior (pero en espera) para un bloqueo exclusivo. Por ejemplo, una instrucción **Update** (que requiere un bloqueo exclusivo) se puede bloquear mediante bloqueos compartidos que se conceden para la serie de instrucciones **Select** . Para resolver un proceso bloqueado (identificado mediante la revisión de [Sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md) DVM), deje de enviar nuevas solicitudes hasta que se haya satisfecho el bloqueo exclusivo.  
  
## <a name="lock-definition-table"></a>Tabla de definición de bloqueo  
SQL Server admite los siguientes tipos de bloqueos. No todos los tipos de bloqueo están disponibles en el nodo de control, pero pueden producirse en los nodos de proceso.  
  
-   SCH-S (estabilidad del esquema). Garantiza que un elemento de un esquema, como una tabla o un índice, no se quite mientras una sesión mantenga un bloqueo de estabilidad del esquema sobre él.  
  
-   SCH-M (modificación del esquema). Debe mantenerlo cualquier sesión que desee cambiar el esquema del recurso especificado. Garantiza que ninguna otra sesión se refiera al objeto indicado.  
  
-   S (compartido). La sesión que lo mantiene recibe acceso compartido al recurso.  
  
-   U (actualizar). Indica que se ha obtenido un bloqueo de actualización sobre recursos que finalmente se pueden actualizar. Se utiliza para evitar una forma común de interbloqueo que tiene lugar cuando varias sesiones bloquean recursos para una posible actualización en el futuro.  
  
-   X (exclusivo). La sesión que lo mantiene recibe acceso exclusivo al recurso.  
  
-   IS (intención compartida). Indica la intención de establecer bloqueos S en algún recurso subordinado de la jerarquía de bloqueos.  
  
-   IU (actualizar intención). Indica la intención de establecer bloqueos U en algún recurso subordinado de la jerarquía de bloqueos.  
  
-   IX (intención exclusiva). Indica la intención de colocar bloqueos X en algunos recursos subordinados en la jerarquía de bloqueos.  
  
-   SIU (actualización de intención compartida). Indica el acceso compartido a un recurso con la intención de obtener bloqueos de actualización sobre recursos subordinados en la jerarquía de bloqueos.  
  
-   SEIS (intención compartida exclusiva). Indica acceso compartido a un recurso con la intención de obtener bloqueos exclusivos sobre recursos subordinados de la jerarquía de bloqueos.  
  
-   UIX (actualizar intención exclusiva). Indica un bloqueo de actualización en un recurso con la intención de adquirir bloqueos exclusivos sobre recursos subordinados en la jerarquía de bloqueos.  
  
-   Bu. Utilizado en las operaciones masivas.  
  
-   RangeS_S (intervalo de claves compartido y bloqueo de recurso compartido). Indica recorrido de intervalo serializable.  
  
-   RangeS_U (intervalo de claves compartido y bloqueo de recurso de actualización). Indica recorrido de actualización serializable.  
  
-   RangeI_N (insertar intervalo de claves y bloqueo de recurso null). Se utiliza para probar los intervalos antes de insertar una clave nueva en un índice.  
  
-   RangeI_S. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y S.  
  
-   RangeI_U. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y U.  
  
-   RangeI_X. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y X.  
  
-   RangeX_S. Bloqueo de conversión de rango de claves, creado por una superposición de bloqueos RangeI_N y RangeS_S pestillo.  
  
-   RangeX_U. Bloqueo de conversión de intervalo de claves, creado por una superposición de bloqueos RangeI_N y RangeS_U.  
  
-   RangeX_X (intervalo de claves exclusivo y bloqueo de recurso exclusivo). Es un bloqueo de conversión que se utiliza cuando se actualiza una clave de un intervalo.  
  
## <a name="see-also"></a>Véase también  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Sys. dm_pdw_waits](../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
