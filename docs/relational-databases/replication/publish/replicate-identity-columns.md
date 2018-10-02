---
title: Replicación de columnas de identidad | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identities [SQL Server replication]
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 091ca8ad9fa80876936dcfdc2c7ed0ca687c6aea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688943"
---
# <a name="replicate-identity-columns"></a>Replicar columnas de identidad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando asigna una propiedad IDENTITY a una columna, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera automáticamente números que se incrementan secuencialmente para las nuevas filas insertadas en la tabla que contiene la columna de identidad. Para obtener más información, vea [IDENTITY &#40;propiedad &#41; &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql-identity-property.md). Debido a que las columnas de identidad pueden estar incluidas como parte de la clave principal, resulta importante evitar los valores duplicados en las columnas de identidad. Para utilizar columnas de identidad en una topología de replicación que tenga actualizaciones en más de un nodo, cada nodo de la topología de replicación debe usar diferentes valores en el intervalo de identidad con el fin de que no se produzcan duplicados.  
  
 Por ejemplo, podría asignarse el rango 1-100 al Publicador, el rango 101-200 al Suscriptor A y el rango 201-300 al Suscriptor B. Si se inserta una fila en el Publicador y el valor de identidad es, por ejemplo, 65, ese valor se replica en cada Suscriptor. Cuando la replicación inserta datos en cada suscriptor, no incrementa el valor de la columna de identidad en la tabla del suscriptor; en su lugar, se inserta el valor literal 65. Son solo las inserciones del usuario y no las del agente de replicación las que hacen que se incremente el valor de la columna de identidad.  
  
 La replicación controla las columnas de identidad en todos los tipos de publicaciones y suscripciones, permitiéndole a usted administrar las columnas manualmente o hacer que la replicación las administre automáticamente.  
  
> [!NOTE]  
>  No se admite la posibilidad de agregar una columna de identidad a una tabla publicada porque puede dar como resultado la falta de convergencia cuando la columna se replica en el suscriptor. Los valores de la columna de identidad en el publicador dependen del orden en que se almacenen físicamente las filas de la tabla afectada. Las filas se pueden almacenar de forma diferente en el suscriptor; por tanto, el valor de la columna de identidad puede ser diferente para las mismas filas.  
  
## <a name="specifying-an-identity-range-management-option"></a>Especificar una opción de administración del intervalo de identidad  
 La replicación ofrece tres opciones de administración del intervalo de identidad:  
  
-   Automático. Se utiliza para replicación de mezcla y replicación transaccional con actualizaciones en el suscriptor. Especifique intervalos de tamaño para el publicador y los suscriptores, y la replicación automáticamente administrará las asignaciones de los nuevos intervalos. La replicación establece la opción NOT FOR REPLICATION en la columna de identidad en el suscriptor, con el fin de que solo las inserciones del usuario hagan que el valor se incremente en el suscriptor.  
  
    > [!NOTE]  
    >  Los suscriptores deben estar sincronizados con el publicador para recibir nuevos intervalos. Como a los suscriptores se les asignan intervalos de identidad automáticamente, es posible que cualquier suscriptor agote todo el suministro de intervalos de identidad si solicita repetidas veces nuevos intervalos.  
  
-   Manual. Se utiliza para replicación de instantáneas y transaccional sin actualizaciones en el suscriptor, replicación transaccional punto a punto o en los casos en los que la aplicación deba controlar los intervalos de identidad mediante programación. Si especifica la administración manual, debe asegurarse de que los intervalos se asignan al publicador y a cada suscriptor y que los nuevos intervalos se asignan si se utilizan los intervalos iniciales. La replicación establece la opción NOT FOR REPLICATION en la columna de identidad en el suscriptor.  
  
-   Ninguno. Esta opción solo se recomienda para lograr la compatibilidad con versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y solo está disponible desde la interfaz de procedimientos almacenados de publicaciones transaccionales.  
  
 Para especificar una opción de administración del intervalo de identidad, vea [Administrar columnas de identidad](../../../relational-databases/replication/publish/manage-identity-columns.md).  
  
## <a name="assigning-identity-ranges"></a>Asignar intervalos de identidad  
 La replicación de mezcla y la replicación transaccional utilizan métodos diferentes para asignar intervalos. Estos métodos se describen en esta sección.  
  
 Existen dos tipos de intervalos que deben tenerse en cuenta a la hora de replicar columnas de identidad: los intervalos asignados al publicador y a los suscriptores, y el intervalo del tipo de datos de la columna. En la siguiente tabla se muestran los intervalos disponibles para los tipos de datos que se utilizan normalmente en las columnas de identidad. El intervalo se utiliza en todos los nodos de una topología. Por ejemplo, si utiliza **smallint** comenzando por 1 con un incremento de 1, el número máximo de inserciones es de 32.767 para el publicador y todos los suscriptores. El número real de inserciones depende de si hay espacios en los valores utilizados y de si se ha utilizado un valor de umbral. Para obtener más información acerca de los umbrales, vea las secciones "Replicación de mezcla" y "Replicación transaccional con suscripciones de actualización en cola" más adelante.  
  
 Si el publicador agota su intervalo de identidad después de una inserción, puede asignar automáticamente un nuevo intervalo si la inserción la realizó un miembro del rol fijo de base de datos **db_owner** . Si la inserción la realizó un usuario con otro rol, el Agente de registro del LOG, el Agente de mezcla o un usuario miembro del rol **db_owner**, deberá ejecutar [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md). Para las publicaciones transaccionales, el Agente de registro del LOG debe estar ejecutándose para asignar automáticamente un nuevo intervalo (la opción predeterminada es que el agente se ejecute continuamente).  
  
> [!WARNING]  
>  Durante una inserción por lotes grande, el desencadenador de replicación se desencadena una sola vez, no para cada fila de la inserción. Esto puede provocar un error en la instrucción de inserción si se agota un intervalo de identidad durante una inserción grande, como una instrucción **INSERT INTO** .  
  
|Tipo de datos|Intervalo|  
|---------------|-----------|  
|**tinyint**|No se admite para la administración automática|  
|**smallint**|De -2^15 (-32.768) a 2^15-1 (32.767)|  
|**int**|De -2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647)|  
|**bigint**|De -2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807)|  
|**decimal** y **numeric**|De -10^38+1 a 10^38-1|  
  
> [!NOTE]  
>  Para crear un número que se incremente automáticamente y que se pueda usar en varias tablas, o que se pueda llamar desde las aplicaciones sin hacer referencia a ninguna tabla, vea [Números de secuencia](../../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
### <a name="merge-replication"></a>Replicación de mezcla  
 Los intervalos de identidad los administra el publicador y se propagan a los suscriptores mediante el Agente de mezcla (en una jerarquía de republicación, los intervalos los administra el publicador raíz y los republicadores). Los valores de identidad se asignan a partir de un grupo en el publicador. Cuando agregue un artículo con una columna de identidad a una publicación en el Asistente para nueva publicación o mediante [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especifique valores para:  
  
-   El parámetro **@identity_range** , que controla el tamaño del intervalo de identidad inicialmente asignado al publicador y a los suscriptores con suscripciones de cliente.  
  
    > [!NOTE]  
    >  En los suscriptores que se ejecuten en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este parámetro (y no el parámetro **@pub_identity_range** ) también controla el tamaño del intervalo de identidad en los suscriptores que se pueden volver a publicar.  
  
-   El parámetro **@pub_identity_range** , que controla el tamaño del intervalo de identidad para las republicaciones asignadas a los suscriptores con suscripciones de servidor (requerido para volver a publicar datos). Todos los suscriptores con suscripciones de servidor reciben un intervalo para volver a publicar, incluso si no han vuelto a publicar ningún dato.  
  
-   El parámetro **@threshold** , que se utiliza para determinar cuándo se requiere un nuevo intervalo de identidades para una suscripción a [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o a una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Por ejemplo, puede especificar 10000 para **@identity_range** y 500000 para **@pub_identity_range**. El publicador y todos los suscriptores que ejecutan [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior, incluido el suscriptor con la suscripción de servidor, están asignados un intervalo principal de 10000. Al suscriptor con la suscripción de servidor también se le asigna un intervalo principal de 500000, que pueden usar los suscriptores que se sincronizan con el suscriptor de republicación (también se debe especificar **@identity_range**, **@pub_identity_range**y **@threshold** para los artículos de la publicación en el suscriptor de republicación).  
  
 Todos los suscriptores que se ejecutan en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o una versión posterior también reciben un intervalo de identidad secundario. El intervalo secundario tiene el mismo tamaño que el intervalo principal. Cuando se agota el intervalo principal, se utiliza el intervalo secundario y el Agente de mezcla asigna un nuevo intervalo en el suscriptor. El nuevo intervalo se convierte en el intervalo secundario y el proceso continúa a medida que el suscriptor utiliza valores de identidad.  
  
  
### <a name="transactional-replication-with-queued-updating-subscriptions"></a>Replicación transaccional con suscripciones de actualización en cola  
 El distribuidor administra los intervalos de identidad y el Agente de distribución los propaga a los suscriptores. Los valores de identidad se asignan a partir de un grupo en el distribuidor. El tamaño del grupo se basa en el tamaño del tipo de datos y en el incremento utilizado para la columna de identidad. Cuando agregue un artículo con una columna de identidad a una publicación en el Asistente para nueva publicación o mediante [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md), especifique valores para:  
  
-   El parámetro **@identity_range** , que controla el tamaño del intervalo de identidad inicialmente asignado a todos los suscriptores.  
  
-   El parámetro **@pub_identity_range** , que controla el tamaño del intervalo de identidad asignado al publicador.  
  
-   El parámetro **@threshold** , que se utiliza para determinar cuándo se requiere un nuevo intervalo de identidades para una suscripción.  
  
 Por ejemplo, puede especificar 10000 para **@pub_identity_range**, 1000 para **@identity_range** (suponiendo menos actualizaciones en el suscriptor), y 80 por ciento para **@threshold**. Después de 800 inserciones en el suscriptor (80 por ciento de 1000), al suscriptor se le asigna un nuevo intervalo. Después de 8000 inserciones en el publicador, al publicador se le asigna un nuevo intervalo. Cuando se asigne un nuevo intervalo, habrá un espacio en los valores del intervalo de identidad de la tabla. Si se especifica un umbral mayor, se obtienen menos espacios pero el sistema es menos tolerante a los errores: si el Agente de distribución no se puede ejecutar por alguna razón, es más fácil que un suscriptor se quede sin identidades.  
  
## <a name="assigning-ranges-for-manual-identity-range-management"></a>Asignar intervalos para la administración manual del intervalo de identidad  
 Si especifica la administración manual del intervalo de identidad, debe asegurarse de que el publicador y todos los suscriptores utilizan intervalos de identidad diferentes. Por ejemplo, imagine una tabla en el publicador con una columna de identidad definida como `IDENTITY(1,1)`: la columna de identidad comienza en 1 y se incrementa en 1 cada vez que se inserta una fila. Si la tabla del publicador tiene 5.000 filas y prevé que aumentará durante la vida de la aplicación, el publicador podría utilizar el rango 1-10.000. Si hay dos suscriptores, el Suscriptor A podría usar el rango 10.001–20.000 y el Suscriptor B, el rango 20.001-30.000.  
  
 Después de inicializar un suscriptor mediante una instantánea u otro medio, ejecute DBCC CHECKIDENT para asignarle al suscriptor un punto de partida para este intervalo de identidad. Por ejemplo, en el suscriptor A, ejecutaría `DBCC CHECKIDENT('<TableName>','reseed',10001)`. En el suscriptor B, ejecutaría `CHECKIDENT('<TableName>','reseed',20001)`.  
  
 Para asignar nuevos intervalos en el publicador o en los suscriptores, ejecute DBCC CHECKIDENT y especifique un valor nuevo para regenerar la tabla. Debería encontrar una manera de determinar cuándo se debe asignar un intervalo nuevo. Por ejemplo, su aplicación podría tener un mecanismo que detectara si un nodo va a consumir su intervalo y asignarle uno nuevo utilizando DBCC CHECKIDENT. También puede agregar una restricción CHECK para asegurarse de que no se pueda agregar una fila si va a ocasionar el uso de un valor fuera del intervalo de identidad.  
  
## <a name="handling-identity-ranges-after-a-database-restore"></a>Controlar los intervalos de identidad tras la restauración de una base de datos  
 Si está utilizando la administración automática del intervalo de identidad, cuando un suscriptor se restaura de una copia de seguridad, automáticamente solicita un nuevo intervalo de valores de identidad. Si un publicador se restaura de una copia de seguridad, debe asegurarse de que al publicador se le ha asignado un intervalo adecuado. Para la replicación de mezcla, asigne un nuevo intervalo con [sp_restoremergeidentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql.md). En la replicación transaccional, determine el valor más alto que se ha utilizado y después establezca el punto de partida para nuevos intervalos. Utilice el siguiente procedimiento después de la restauración de la base de datos de publicaciones:  
  
1.  Detenga todas las actividades en todos los suscriptores.  
  
2.  Por cada tabla publicada que incluya una columna de identidad:  
  
    1.  En la base de datos de suscripciones en cada suscriptor, ejecute `IDENT_CURRENT('<TableName>')`.  
  
    2.  Registre el valor más alto encontrado en todos los suscriptores.  
  
    3.  En la base de datos de publicaciones en el publicador, ejecute `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`.  
  
    4.  En la base de datos de publicaciones en el publicador, ejecute `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`.  
  
    > [!NOTE]  
    >  Si el valor de la columna de identidad está establecido para que se reduzca y no para que se incremente, registre el valor más bajo encontrado y regenere con ese valor.  
  
## <a name="see-also"></a>Ver también  
 [BACKUP &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENTITY &#40;propiedad&#41; &#40;Transact-SQL&#41;](../../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql.md)  
  
  
