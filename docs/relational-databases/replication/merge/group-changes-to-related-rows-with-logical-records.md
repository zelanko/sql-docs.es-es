---
title: "Agrupar cambios en filas relacionadas con registros lógicos | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication logical records [SQL Server replication]
- articles [SQL Server replication], logical records
- logical records [SQL Server replication]
ms.assetid: ad76799c-4486-4b98-9705-005433041321
caps.latest.revision: "55"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 026199b68479b9219984123bcc5958b037474986
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="group-changes-to-related-rows-with-logical-records"></a>Agrupar cambios en filas relacionadas con registros lógicos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 De manera predeterminada, la replicación de mezcla procesa los cambios de datos fila por fila. Esto es apropiado en muchos casos, pero para algunas aplicaciones, es fundamental que las filas relacionadas se procesen como una unidad. La característica de registros lógicos de la replicación de mezcla permite definir una relación entre filas relacionadas de diferentes tablas, para que las filas se procesen como una unidad.  
  
> [!NOTE]  
>  La característica de registros lógicos se puede utilizar sola o con los filtros de combinación. Para obtener más información acerca de los filtros de combinación, vea [Join Filters](../../../relational-databases/replication/merge/join-filters.md). Para utilizar los registros lógicos, el nivel de compatibilidad de la publicación debe ser de al menos 90RTM.  
  
 Considere estas tres tablas relacionadas:  
  
 ![Tres registros lógicos de tabla, solo con los nombres de columna](../../../relational-databases/replication/merge/media/logical-records-01.gif "Tres registros lógicos de tabla, solo con los nombres de columna")  
  
 La tabla **Customers** es la tabla primaria en esta relación y tiene una columna de clave principal, **CustID**. La tabla **Orders** tiene una columna de clave principal, **OrderID**, con una restricción de clave externa en la columna **CustID** que hace referencia a la columna **CustID** de la tabla **Customers** . De la misma forma, la tabla **OrderItems** tiene una columna de clave principal, **OrderItemID**, con una restricción de clave externa en la columna **OrderID** que hace referencia a la columna **OrderID** de la tabla **Orders** .  
  
 En este ejemplo, un registro lógico está formado por todas las filas de la tabla **Orders** relacionadas con un solo valor **CustID** y todas las filas de la tabla **OrderItems** relacionadas con esas filas en la tabla **Orders** . En este diagrama se muestran todas las filas de las tres tablas que se incluyen en el registro lógico para Customer2:  
  
 ![Tres registros lógicos de tabla con valores](../../../relational-databases/replication/merge/media/logical-records-02.gif "Tres registros lógicos de tabla con valores")  
  
 Para definir una relación lógica entre artículos, vea [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
## <a name="benefits-of-logical-records"></a>Ventajas de los registros lógicos  
 La característica de registros lógicos tiene dos ventajas principales:  
  
-   Los cambios de datos se aplican como una unidad.  
  
-   Los conflictos se detectan y resuelven simultáneamente en varias filas de varias tablas.  
  
### <a name="the-application-of-changes-as-a-unit"></a>Aplicación de cambios como una unidad  
 Si se utilizan registros lógicos y se interrumpe el proceso de mezcla, como ocurre en el caso de que se termine la conexión, se revierte el conjunto de cambios relacionados replicados parcialmente. Por ejemplo, considere el caso en el que un suscriptor agrega un nuevo pedido con **OrderID** = 6 y dos filas nuevas a la tabla **OrderItems** con **OrderItemID** = 10 y **OrderItemID** = 11 para **OrderID** = 6.  
  
 ![Tres registros lógicos de tabla con valores](../../../relational-databases/replication/merge/media/logical-records-04.gif "Tres registros lógicos de tabla con valores")  
  
 Si no se utilizan registros lógicos y el proceso de replicación se interrumpe después de finalizar la fila **Orders** para **OrderID** = 6 pero antes de finalizar **OrderItems** 10 y 11, el valor de **OrderTotal** para **OrderID** = 6 no será coherente con la suma de los valores **OrderAmount** de las filas **OrderItems** . Si se utilizan registros lógicos, la fila **Orders** para **OrderID** = 6 no se confirma hasta que se repliquen los cambios de **OrderItems** relacionados.  
  
 En un escenario distinto, si se utilizan registros lógicos y alguien está consultando las tablas cuando el proceso de mezcla está aplicando cambios, el usuario no verá los cambios parcialmente replicados hasta que finalicen. Por ejemplo, el proceso de replicación ha cargado la fila Orders para **OrderID** = 6, pero un usuario consulta las tablas antes de que el proceso de replicación haya replicado las filas **OrderItems** . En este caso, el valor **OrderTotal** no será igual a la suma de los valores **OrderAmount** . Si se utilizan registros lógicos, la fila **Orders** no estará visible hasta que finalicen las filas **OrderItems** y la transacción se confirme como una unidad.  
  
### <a name="the-application-of-conflict-handling-to-more-than-one-table"></a>Aplicación del control de conflictos a más de una tabla  
 Considere el caso en el que dos suscriptores tienen el conjunto de datos anterior:  
  
-   Un usuario del primer suscriptor cambia **OrderAmount** de **OrderItemID** 5 de 100 a 150 y **OrderTotal** de **OrderID** 3 de 200 a 250.  
  
-   Un usuario del segundo suscriptor cambia **OrderAmount** de **OrderItemID** 6 de 25 a 125 y **OrderTotal** de **OrderID** 3 de 200 a 300.  
  
 Si estos cambios se replican sin utilizar registros lógicos, los diferentes valores de **OrderTotal** producirán un conflicto y solo se replicará uno de ellos. Sin embargo, los cambios que no tengan conflictos en la tabla **OrderItems** se replicarán sin conflictos, lo que dejará los valores finales de **OrderTotal** en un estado incoherente respecto a las filas **OrderItems** . Si se utilizan registros lógicos en este escenario, también se revertirá el cambio de **OrderItems** asociado a la tabla **Orders** perdedora y el valor final de **OrderTotal** será un resumen exacto de las filas **OrderItems** .  
  
 Para obtener más información sobre las opciones relacionadas con la detección y resolución de conflictos con registros lógicos, vea [Detectar y solucionar conflictos en registros lógicos](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
## <a name="considerations-for-using-logical-records"></a>Consideraciones para el uso de registros lógicos  
 Tenga en cuenta las consideraciones siguientes al utilizar registros lógicos:  
  
### <a name="general-considerations"></a>Consideraciones generales  
  
-   Se recomienda mantener el menor número de tablas posible en un registro lógico; se recomienda utilizar cinco tablas o menos.  
  
-   Los registros lógicos no pueden hacer referencia a columnas con ninguno de los siguientes tipos de datos:  
  
    -   **varchar(max)** y **nvarchar(max)**  
  
    -   **varbinary(max)**  
  
    -   **text** y **ntext**  
  
    -   **imagen**  
  
    -   **XML**  
  
    -   **UDT**  
  
-   Las relaciones de clave externa en las tablas publicadas no se pueden definir con la opción CASCADE. Para obtener más información, vea [CREATE TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql.md) y [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md).  
  
-   No puede actualizar columnas que se utilicen en una cláusula de relación lógica.  
  
-   No se admite la resolución de conflictos personalizada con controladores de lógica de negocios o solucionadores personalizados para los artículos incluidos en un registro lógico.  
  
-   Si se utilizan registros lógicos en una publicación que incluye filtros con parámetros, debe inicializar cada suscripción con una instantánea para su partición. Si inicializa un suscriptor con otro método, se producirá un error en el Agente de mezcla. Para más información, consulte [Snapshots for Merge Publications with Parameterized Filters](../../../relational-databases/replication/snapshots-for-merge-publications-with-parameterized-filters.md).  
  
-   Los conflictos que implican registros lógicos no se muestran en el Visor de conflictos. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, consulte [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
### <a name="publication-settings"></a>Configuración de publicaciones  
  
-   La publicación debe tener un nivel de compatibilidad igual o superior a 90RTM. Para obtener más información, vea la sección sobre el nivel de compatibilidad de las publicaciones en el tema [Replication Backward Compatibility](../../../relational-databases/replication/replication-backward-compatibility.md)(Compatibilidad con versiones anteriores de replicación).  
  
-   La publicación debe utilizar un modo de instantánea nativo. Ésta es la opción predeterminada, a menos que esté replicando en [!INCLUDE[ssEW](../../../includes/ssew-md.md)], que no admite registros lógicos.  
  
-   La publicación no permite la sincronización web. Para obtener más información acerca de la sincronización web, vea [Web Synchronization for Merge Replication](../../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
-   Para utilizar registros lógicos en una publicación filtrada:  
  
    -   También debe utilizar particiones precalculadas. Los requisitos de las particiones precalculadas también se aplican a los registros lógicos. Para obtener más información, vea [Optimización del rendimiento de los filtros con parámetros con particiones calculadas previamente](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md).  
  
    -   No puede utilizar filtros con parámetros no superpuestos. Para obtener más información, vea la sección la sección sobre cómo establecer opciones de partición en el tema [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
-   Si la publicación utiliza filtros de combinación, debe establecer la propiedad **join unique key** en **true** para todos los filtros de combinación involucrados en relaciones de registros lógicos. Para más información, consulte [Join Filters](../../../relational-databases/replication/merge/join-filters.md).  
  
### <a name="relationships-between-tables"></a>Relaciones entre tablas  
  
-   Las tablas relacionadas a través de registros lógicos deben tener una relación clave principal-clave externa.  
  
-   No se puede establecer la opción NOT FOR REPLICATION para restricciones de clave externa.  
  
-   Las tablas secundarias solo pueden tener una tabla primaria.  
  
     Por ejemplo. una base de datos que realice un seguimiento de las clases y los estudiantes puede tener un diseño similar al siguiente:  
  
     ![Tabla secundaria con más de una tabla primaria](../../../relational-databases/replication/merge/media/logical-records-03.gif "Tabla secundaria con más de una tabla primaria")  
  
     No puede utilizar un registro lógico para representar las tres tablas en esta relación, ya que las filas de **ClassMembers** no están asociadas con una sola fila de clave principal. Las tablas **Classes** y **ClassMembers** pueden formar un registro lógico, al igual que las tablas **ClassMembers** y **Students**, pero no las tres juntas.  
  
-   La publicación no puede contener relaciones circulares de filtros de combinación.  
  
     Siguiendo el ejemplo de las tablas **Customers**, **Orders**y **OrderItems**, no puede utilizar registros lógicos si la tabla **Orders** también tiene una restricción de clave externa que hace referencia a la tabla **OrderItems** .  
  
## <a name="performance-implications-of-logical-records"></a>Consecuencias de los registros lógicos en el rendimiento  
 La característica de registros lógicos tiene un costo en rendimiento. Si no se utilizan registros lógicos, el agente de replicación puede procesar todos los cambios para un artículo determinado a la vez, y como los cambios se aplican fila por fila, los requisitos de bloqueo y registro de transacciones necesarios para aplicar los cambios son mínimos.  
  
 Si se utilizan registros lógicos, el Agente de mezcla debe procesar juntos los cambios de todo el registro lógico. Esto afecta al tiempo que tarda el Agente de mezcla en replicar las filas. Además, como el agente abre una transacción distinta para cada registro lógico, los requisitos de bloqueo pueden aumentar.  
  
## <a name="see-also"></a>Vea también  
 [Article Options for Merge Replication](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
  
