---
title: Publicación de la ejecución de procedimientos almacenados en la replicación transaccional | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- publishing [SQL Server replication], stored procedure execution
- articles [SQL Server replication], stored procedures and
- transactional replication, publishing stored procedure execution
ms.assetid: f4686f6f-c224-4f07-a7cb-92f4dd483158
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 85643186d92e2033fc909ae166533cac0e18f44d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732713"
---
# <a name="publishing-stored-procedure-execution-in-transactional-replication"></a>Publicar la ejecución de procedimientos almacenados en la replicación transaccional
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si tiene uno o más procedimientos almacenados que se ejecutan en el publicador y afectan a las tablas publicadas, considere la posibilidad de incluir esos procedimientos en la publicación como artículos de ejecución de procedimientos almacenados. La definición del procedimiento (la instrucción CREATE PROCEDURE) se replica en el suscriptor cuando se inicializa la suscripción; cuando el procedimiento se ejecuta en el publicador, la replicación ejecuta el procedimiento correspondiente en el suscriptor. Esto puede proporcionar un rendimiento significativamente mejor en los casos en los que se llevan a cabo grandes operaciones por lotes, debido a que únicamente se replica la ejecución del procedimiento, evitando la necesidad de replicar los cambios individuales de cada fila. Por ejemplo, supongamos que crea el siguiente procedimiento almacenado en la base de datos de publicaciones:  
  
```  
CREATE PROC give_raise AS  
UPDATE EMPLOYEES SET salary = salary * 1.10  
```  
  
 Este procedimiento aumenta el salario de los 10.000 empleados de la compañía en un 10 por ciento. Cuando ejecute este procedimiento almacenado en el publicador, actualizará el salario de todos los empleados. Sin la replicación de la ejecución del procedimiento almacenado, la actualización se envía a los suscriptores como una transacción de gran tamaño compuesta por varios pasos:  
  
```  
BEGIN TRAN  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 1'  
UPDATE EMPLOYEES SET salary = salary * 1.10 WHERE PK = 'emp 2'  
```  
  
 Y esto se repite para 10.000 actualizaciones.  
  
 Con la replicación de la ejecución del procedimiento almacenado, la replicación solo envía el comando para ejecutar el procedimiento almacenado en el suscriptor, en vez de tener que escribir todas las actualizaciones en la base de datos de distribución y enviarlas después a través de la red al suscriptor:  
  
```  
EXEC give_raise  
```  
  
> [!IMPORTANT]  
>  La replicación de procedimientos almacenados no es apropiada para todas las aplicaciones. Si se filtra un artículo de forma horizontal, de modo que existen conjuntos de filas diferentes en el publicador y en el suscriptor, la ejecución del mismo procedimiento almacenado en ambos produce resultados diferentes. De forma similar, si una actualización se basa en una subconsulta de otra tabla no replicada, la ejecución del mismo procedimiento almacenado en ambos produce resultados diferentes.  
  
 **Para publicar la ejecución de un procedimiento almacenado**  
  
-   SQL Server Management Studio: [Publicar la ejecución de un procedimiento almacenado en una publicación transaccional &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
-   Programación de la replicación con Transact-SQL: ejecute [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) y especifique un valor "serializable proc exec" (recomendado) o "proc exec" para el parámetro **@type**. Para obtener más información sobre la definición de artículos, vea [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="modifying-the-procedure-at-the-subscriber"></a>Modificar el procedimiento en el suscriptor  
 De forma predeterminada, la definición del procedimiento almacenado del publicador se propaga a todos los suscriptores. No obstante, también puede modificar el procedimiento almacenado en el suscriptor. Esto es útil si desea ejecutar una lógica diferente en el publicador y en el suscriptor. Por ejemplo, observe **sp_big_delete**, un procedimiento almacenado en el publicador que tiene dos funciones: elimina 1.000.000 de filas de la tabla replicada **big_table1** y actualiza la tabla no replicada **big_table2**. Para reducir la demanda de recursos de red, debe propagar la eliminación del millón de filas como un procedimiento almacenado mediante la publicación de **sp_big_delete**. En el suscriptor, puede modificar **sp_big_delete** de forma que solamente elimine el millón de filas y no haga la posterior actualización de la tabla **big_table2**.  
  
> [!NOTE]  
>  De forma predeterminada, los cambios efectuados mediante ALTER PROCEDURE en el publicador se propagan al suscriptor. Para evitarlo, deshabilite la propagación de los cambios de esquema antes de ejecutar ALTER PROCEDURE. Para obtener información sobre los cambios de esquema, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="types-of-stored-procedure-execution-articles"></a>Tipos de artículos de ejecución de procedimientos almacenados  
 Hay dos maneras diferentes en las que se puede publicar la ejecución de un procedimiento almacenado: artículo de ejecución de procedimiento serializable y artículo de ejecución de procedimiento.  
  
-   Se recomienda la opción serializable puesto que replica la ejecución del procedimiento solamente si éste se ejecuta dentro del contexto de una transacción serializable. Si el procedimiento almacenado se ejecuta fuera de una transacción serializable, los cambios efectuados en los datos de las tablas publicadas se replican como una serie de instrucciones DML. Este comportamiento contribuye a hacer que los datos del suscriptor sean coherentes con los datos del publicador. Esto es especialmente útil en operaciones por lotes, como grandes operaciones de limpieza.  
  
-   Con la opción de ejecución del procedimiento, es posible que la ejecución se pueda replicar en todos los suscriptores independientemente de que las instrucciones individuales del procedimiento almacenado se hayan ejecutado correctamente o no. Además, como los cambios que el procedimiento almacenado efectúa en los datos pueden ocurrir en varias transacciones, los datos de los suscriptores podrían no ser coherentes con los del publicador. Para resolver estos problemas, se requiere que los suscriptores sean de solo lectura y que se use un nivel de aislamiento mayor que READ UNCOMMITTED. Si utiliza READ UNCOMMITED, los cambios en los datos de las tablas publicadas se replican como una serie de instrucciones DML.  
  
 En el siguiente ejemplo se ilustra por qué se recomienda configurar la replicación de procedimientos como artículos de procedimientos serializables.  
  
```  
BEGIN TRANSACTION T1  
SELECT @var = max(col1) FROM tableA  
UPDATE tableA SET col2 = <value>   
   WHERE col1 = @var   
  
BEGIN TRANSACTION T2  
INSERT tableA VALUES <values>  
COMMIT TRANSACTION T2  
```  
  
 En el ejemplo anterior, se asume que la instrucción SELECT en la transacción T1 ocurre antes que la instrucción INSERT en la transacción T2.  
  
 Si el proceso no se ejecuta en una transacción serializable (con el valor de nivel de aislamiento establecido en SERIALIZABLE), la transacción T2 podrá insertar una nueva fila en el intervalo de la instrucción SELECT en T1 y se confirmará antes que T1. Esto también quiere decir que se aplicará en el suscriptor antes que T1. Cuando se aplica T1 en el suscriptor, la instrucción SELECT puede devolver potencialmente un valor diferente que en el publicador y puede ofrecer un resultado distinto de UPDATE.  
  
 Si el procedimiento se ejecuta en una transacción serializable, la transacción T2 no podrá insertar en el intervalo que abarca la instrucción SELECT en T2. Estará bloqueada hasta que T1 confirme que garantiza los mismos resultados en el suscriptor.  
  
 Los bloqueos se mantendrán hasta que ejecute el procedimiento en una transacción serializable y puede dar como resultado una simultaneidad reducida.  
  
## <a name="the-xactabort-setting"></a>Configuración de XACT_ABORT  
 Al replicar la ejecución del procedimiento almacenado, la configuración de la sesión que ejecuta el procedimiento almacenado debe especificar XACT_ABORT ON. Si XACT_ABORT se establece en OFF, y se produce un error durante la ejecución del procedimiento en el publicador, el mismo error ocurrirá en el suscriptor y el Agente de distribución no funcionará. Si se especifica XACT_ABORT ON, se garantiza que cualquier error que se produzca durante la ejecución en el publicador hará que toda la ejecución se revierta, con lo que se evita que se produzca un error en el Agente de distribución. Para obtener más información sobre la configuración de XACT_ABORT, vea [SET XACT_ABORT &#40;Transact-SQL&#41;](../../../t-sql/statements/set-xact-abort-transact-sql.md).  
  
 Si necesita una configuración de XACT_ABORT OFF, especifique el parámetro **-SkipErrors** para el Agente de distribución. De esta forma permitirá que el agente continúe aplicando cambios en el suscriptor incluso si se produce un error.  
  
## <a name="see-also"></a>Ver también  
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
